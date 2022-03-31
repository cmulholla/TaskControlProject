# TaskControlProject
project number 2 for my operating systems class

# Project PDF
Project Task_Control (100 points) 
Create a program that simulates a simple operating system task control. The task control must 
have 3 states: Ready, Run, and Wait states. The program will start with zero tasks and terminates 
when the maximum number of tasks have been simulated. The state diagram is shown below. 
 
 To handle the task control, you need to create two dynamic linked lists, i.e., a wait queue, and a 
ready queue, to store the task control blocks (TCB). The ready queue should follow the first in 
first out (FIFO) algorithm. Each process must have its own TCB object with the following object 
members. Below shows an example (this is not a comprehensive list): 
```
• Task number - this is the unique task ID (TID). 
• CPU time – total run time spend executed by the CPU. 
• Burst time – allowed time to run before the task gets blocked. 
• Block time – the time that a task must spend waiting for an I/O. 
• Wall time – the time a task spends from dispatch until it terminates. 
• Start and end wall time. 
• Accumulated burst time. 
• ...... 
 ```
You  will  simulate  a  timeline  in  this  project,  with  the  simulation  starting  at  tick  0.  Before  the 
simulation, you will pick five random numbers as task creation times. For example: 
T = {5, 17, 32, 80, 134} 
At the selected time you will create a new task. E.g., create 1st task at tick 5, 2nd task at tick 17, ......; you 
will create five tasks accordingly. When a new task is created, generate a task number, a random CPU 
time, a random burst time, and a random block time in TCB, and push it into the ready queue. The task 
number (TID) will start with 1. i.e., TID = 1, 2, 3, 4, 5 for the five tasks. When a task enters the ready queue 
for  the  first  time,  its wall  time  starts.  Simulation  always  dispatches  one  task  if the  CPU  is  idle.  When  a 
task’s burst time expires, it enters the wait queue. This simulates a task being interrupted for I/O wait 
time. When a task’s block time expires, it enters the read queue again. Note that this routine may repeat 
several times until the accumulated burst time reaches the CPU time, i.e., the task terminates and its wall 
time ends. \n
 
Below shows a comprehensive task control scenario with 2 random tasks T = {0, 50}: \n
``` 
At tick 0, create the first task T1 with TCB1 as shown below, and push T1 into ready queue, update the 
start wall time of T1 = 0; Since the CPU is idle, we dispatch T1 into running and count down its burst time; 

TID: 1 
CPU time: 30 
Burst time: 10 
Block time: 40 
Wall time: 
Start wall time: 
End wall time: 
Accumulated burst: 
 
At  tick  10,  since  burst  time  of  T1  expires,  we  push  T1  into  wait  queue  and  count  down  its  block  time. 
Update the accumulated burst of T1 = 10; 
 
At tick 50, create the second task T2 with TCB2 as shown below, and push T2 into ready queue. Update 
the start wall time of T2 = 50; Since block time of T1 expires, we push T1 into ready queue again. Note 
that the ready queue is a FIFO linked list, if here comes multiple tasks we always push the newly created 
task first. So far, we have TCB2 -> TCBj1 in the ready queue; Since the CPU is idle, we pop and dispatch T2 
into running and count down its burst time; 

TID: 2 
CPU time: 40 
Burst time: 20 
Block time: 100 
Wall time: 
Start wall time: 
End wall time: 
Accumulated burst: 

At  tick  70,  since  burst  time  of  T2  expires,  we  push  T2  into  wait  queue  and  count  down  its  block  time. 
Update the accumulated burst of T2 = 20; Since the CPU is idle, we pop and dispatch T1 into running and 
count down its burst time; 
 
At  tick  80,  since  burst  time  of  T1  expires,  we  push  T1  into  wait  queue  and  count  down  its  block  time. 
Update the accumulated burst of T1 = 20; 
 
At tick 120, since block time of T1 expires, we push T1 into ready queue again; Since the CPU is idle, we 
pop and dispatch T1 into running and count down its burst time; 
 
At tick 130, since the accumulated burst time of T1 reaches 30 – the predefined CPU time, T1 terminates. 
Update the end wall time of T1 = 130, calculate the wall time of T1 = end wall time – start wall time = 130 
– 0 = 130; We can calculate a ratio of CPU/wall time = 23.08%; 
 
At tick 170, since block time of T2 expires, we push T2 into ready queue again; Since the CPU is idle, we 
pop and dispatch T2 into running and count down its burst time; 
 
At tick 190, since the accumulated burst time of T2 reaches 40 – the predefined CPU time, T2 terminates. 
Update the end wall time of T2 = 190, calculate the wall time of T2 = end wall time – start wall time = 190 
– 50 = 140; We can calculate a ratio of CPU/wall time = 28.57%. 
 
Since all tasks are terminated, simulation ends. 
 
Output the simulation results to the screen.  A typical output might look like the following: 

Task Number Wall Time CPU time  % CPU/Wall Time
1           2235      400       5.3 
3           17131     477       3.2 
11          24788     1386      4.6 
7           26601     2063      7.4 
...... 
```
