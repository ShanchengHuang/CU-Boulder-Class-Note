# IPC 

## Types of Shared Resources

- Files
- Memory
- Peripherals
- External Hardware Devices
- Other?

### Not just resource
- Steps
  


## Mutal Exclusion  
- Coordination  
- Synchronization  
- Condition Flag  
- Condition Flag group  

### Semaohore-信号量  
- Acquiring/Receiving
- Releasing/Sending

Creating a semaphore
```
void OSSemCreate(OS_SEM* p_sem, CPU_CHAR* p_name,
OS_SEM_CTR cnt, RTOS_ERR* p_err);
```
Acquiring (and possibly waiting for) a semaphore. Calling task
may block.
```
OS_SEM_CTR OSSemPend(OS_SEM* p_sem, OS_TICK
timeout, OS_OPT opt, CPU_TS* p_ts, RTOS_ERR* p_err);
```
Releasing (signaling) a semaphore
```
OS_SEM_CTR OSSemPost(OS_SEM* p_sem, OS_OPT opt,
RTOS_ERR* p_err);
```
[opt] can be specified such that on release, either one or all
waiting tasks become ready  

```
OS_EVENT *Isr1Semaphore = null;

/* Create semaphore */
void CreateIsr1Semaphore()
{
    Isr1Semaphore = OSSemCreate(1); /* count = 1 */
}

/* ISR to handle interrupt */
void ISR1()
{
    .....                         /* do stuff pre-SemPost */
        OSSemPost(Isr1Semaphore); /* semaphore to post */
    .....                         /* if more to do */
}

/* Task: the main flow */
void MyTask()
{
    while (1)
    {
        .....
            /* wait for semaphore to continue */
            OSSemPend(Isr1Semaphore, /* semaphore to wait */
                      100,           /* timeout */
                      err);          /* error */
        .....                        /* do stuff post-ISR critical handling */
    }
}

void main()
{
    uint8_t error;
    ...... MotorStartEventGroup = OSFlagCreate(
        0,       /* initial value */
        &error); /* store error */
    ......
}

void MotorTask()
{
    ...... OsFlagPend(MotorStartEventGroup,        /* Wait on this */
                      AlarmEvent + InterLockEvent, /* Events to check */
                      OS_FLAG_WAIT_SET_ALL +       /* till all set */
                          OS_FLAG_CONSUME,         /* then consume */
                      0xFFFF);                     /* time out */
    ......
}

void AlarmTask()
{
    uint8_t error;
    OSFlagPost(MotorStartEventGroup, /* post in this */
               AlarmEvent,           /* Event to set */
               OS_FLAG_SET,          /* set bit */
               &error);              /* error */
}
void InterLockTask()
{
    uint8_t error;
    OSFlagPost(MotorStartEventGroup, /* post in this */
               InterLockEvent,       /* Event to set */
               OS_FLAG_SET,          /* set bit */
               &error);              /* error */
}
```

## Events
- A series of bits in a word to hold current state of the events in the group
- Similar mechanism as Semaphore on Pend and Post
- Multiple tasks may post different flags
- Waiting task may wait for multiple flags (can be OR-ed,AND-ed)

```
OS_EVENT *SemaSync1, SemaSync2;
void main(int argc char *argv[])
{
    .....SemaSync1 = OSSemCreate(0); /* initial value */
    SemaSync2 = OSSemCreate(0);      /* initial value */
    ......
}
void *Task1(void *param)
{
    ...... uint8_t error;
    OSSemPost(SemaSync1);                 /* done w/ my part */
    OSSemPend(SemaSync2, 0xFFFF, &error); /* wait for other */
    ......
}
```

## Pool

Asynchronous info exchages  
Read-Write Random  
Non-Destructive read  
Data may be protected  

## Message Queue

Other name: Channel buffer, pipe  
Asynchronous access  
FIFO  
Can be implementd by linked list 
Fixed memory space  
Reuse memory space   
Sender task may pend when buffer is full  
Reader task may pend when buffer is empty  