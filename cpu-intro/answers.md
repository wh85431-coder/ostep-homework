# OSTEP cpu-intro Homework Answers

## Q1
Prediction: CPU utilization will be 100%.
Reason: Both processes only run CPU instructions, no I/O. The CPU keeps busy executing instructions without idle time.
Result: Total Time 10, CPU Busy 10 (100.00%), IO Busy 0 (0.00%).

## Q2
Prediction: The CPU utilization will be less than 100%. Process 0 runs all 4 CPU instructions first, then process 1 runs its I/O instruction. While waiting for I/O, CPU is idle.
Reason: Process 0 finishes all CPU instructions first. Then process 1 starts I/O and becomes blocked. The CPU has no other ready jobs during I/O waiting time, so CPU utilization drops.
Result: Total Time 11, CPU Busy 6 (54.55%), IO Busy 5 (45.45%).

## Q3
Prediction: CPU utilization will be higher than Q2. While PID0 waits for I/O, PID1 can run its CPU instructions in parallel.
Reason: Process 0 starts I/O first and becomes blocked. The OS switches to process 1, which uses the CPU during the I/O waiting period. This overlaps CPU work and I/O, improving utilization.
Result: Total Time 7, CPU Busy 6 (85.71%), IO Busy 5 (71.43%).

## Q4
Prediction: We can overlap I/O and CPU work between these four instructions. The OS switches to run CPU instruction while another process waits for I/O.
Reason: The sequence is I/O → CPU → I/O → CPU. When one process is blocked on I/O, the scheduler runs the ready CPU task, overlapping computation and I/O to improve resource usage.
Result: Total Time 9, CPU Busy 6 (66.67%), IO Busy 7 (77.78%).

## Q5
Prediction: CPU utilization will drop. Process 0 has three I/O instructions, and process 1 only has one CPU instruction. After PID1 finishes its single CPU task early, there is no ready job left while PID0 waits for I/O.
Reason: PID1 quickly completes and terminates. The rest of the time, only PID0 is running I/O. When PID0 is blocked waiting for I/O completion, no other process can use the CPU, leading to many idle CPU cycles.
Result: Total Time 21, CPU Busy 7 (33.33%), IO Busy 15 (71.43%).

## Q6
Prediction: The result is the same as Q4. SWITCH_ON_IO is already the default scheduler policy for this trace.
Reason: SWITCH_ON_IO means the OS switches context immediately when a process issues an I/O. In this workload, we already switch to ready CPU tasks when I/O starts, so the total time and utilization do not change.
Result: Total Time 9, CPU Busy 6 (66.67%), IO Busy 7 (77.78%).

## Q7
Prediction: The total time and utilization remain unchanged. IO_RUN_LATER controls what happens when an I/O completes, but in this trace, no other process is ready when I/O finishes, so the policy does not affect the timeline.
Reason: IO_RUN_LATER means when an I/O finishes, the system does not immediately run the woken-up process; it only picks a new process when the currently running process stops. In this example, when I/O completes, there is no competing ready process, so scheduling choice makes no difference.
Result: Total Time 9, CPU Busy 6 (66.67%), IO Busy 7 (77.78%).
