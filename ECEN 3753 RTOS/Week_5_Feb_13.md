# Scheduling

- Max thoughput
- Max utilized
- Min Response time
- Min wait time
- Min start a new task
- Share resources appropriately

## Criteria for Scheduling

- CPU Utilization
- Response Time
- Turnaround Time 
- Wait Time


## Non Preemptive Scheduling

- Cooperative multitaskling
- Non-preemptive scheduler

## Preemptive Scheduling

## Scheduling Algorithms

- First-Come, First-served
  - Pros: No context switch
  - Cons: Slow
- Shortest Job First
  - Pro: Max Task throughtput
  - Con: Lager Task potentially would wait forever, hard to konw when the task done.
  - Unit test: 
- Time slice 
  - Pro: Fully deterministic
  - Con: Task has nothing to do during emptry
- Time Slice with Background Tasks
  - Pro: Fully deterministic just like the Time slice, improves time slice.
  - Con: Background tast will never scheduled or Overhead due context switching
- Round Robin
  - Pro: Great for small task
  - Con: hightest priority task not run immediately.
- Priority
  - Pro: High priority run first
  - Con: Low priority can wait very long, overhead due context-switch
  - 


# Memory Management Topics

## Type of Memory
- Volatile
  - Ram
- Non-Volatile
  - Not erasable

|             | SRAM | DRAM |
|-------------|------|------|
| Density     | L    | H    |
| Cost        | H    | L    |
| Speed       | H    | L    |
| mWh         | L    | H    |
| Reliability | H    | l    |

Temporal locality
Spatial localitys

