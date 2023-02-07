# Task
- 100% cycle max consumed
- Coupling

> If a program needs to wait for an operations to complete, a responsible task can block
>  - Blocked task awake up by a interrupt

`Process`
- Heavy

`Thread`
- Light
- Share memory
- Process may spawn one or more process

`Task`
- Light
- Aloowing decoupling


## Diagram

- Data Flow Diagram
- State Machine Diagram
- Sequence Diagram

## Resource

Need the physical CPU  
Porgram counter to instructions to fetch  
Maintain the current state of the program
- what is currently running
- next taks
  
Each task has it own stack, and interrupt also has it own stack

> growth toward '0'

---

`ABI` Application Binary Interface

Parameter R0-R3
Stack point R4

`Stack Frames Pointer`

## Task switch 
- Allocate stack space to save all the the CPU register for the currently running task
- Save SP in the current task's contril block.
- Save the cpu registers
- Load the sp 
- Load any remaining cpu
- Set PC

## Creating Task

- Reserve from task stck
- Task name
- Entry Point
    -   ```
        void entryFunctions(void*)
        ```
- Task priority
- Taks control block


  





