---
layout: project
type: project
image: img/cotton/freertos.png
title: "Implementation of Overload Scheduling Algorithms in FreeRTOS"
date: 2014
published: true
labels:
  - RTOS
  - C
summary: "Implementation of Rate Monotonic Scheduling and Deadline Monotonic Scheduling Algorithms in FreeRTOS"
---

<img class="img-fluid" src="../img/cotton/freertos.png">

Designed a custom scheduler to implement the RMS and DMS (pre-emptive) scheduling algorithm in C based on FreeRTOS.

The summary of the algorithms and implementation is as follows:

<hr>

<pre>

RMS is a priority-based scheduling algorithm used to schedule periodic real-time tasks. It assigns priorities to tasks based on their periods, with shorter periods assigned higher priorities. The fundamental principle of RMS is that tasks with shorter periods have higher priority and are scheduled before tasks with longer periods. This algorithm assumes that the execution times of tasks are known and constant.

Key features of RMS:

- Priority assignment based on task periods.
- Fixed-priority scheduling.
- Assumes deterministic task execution times.
- Preemptive scheduling (higher priority tasks can preempt lower priority tasks).
- Guarantees the schedulability of a set of tasks if their total utilization is less than a certain threshold (around 69%).

Deadline Monotonic Scheduling (DMS):
DMS is also a priority-based scheduling algorithm used for real-time systems. Like RMS, it assigns priorities to tasks based on their deadlines. However, unlike RMS, DMS does not assume deterministic execution times. Instead, it focuses on meeting task deadlines, considering the worst-case execution time.
Key features of DMS:

- Priority assignment based on task deadlines.
- Fixed-priority scheduling.
- Considers worst-case execution times.
- Preemptive scheduling.
- Guarantees the schedulability of a set of tasks if their total utilization is less than a certain threshold (around 100%).


- The algorithm does not need to perform any schedulability test.
- In the event that a job misses its deadline, it is suspended and runs as a new job at its next release time. In other words, the current (missed) instance of the task is dropped.
- The code prints out relevant information to the serial monitor, e.g., which task is executing, if a task misses its deadline, etc.
- If a job executes for more than its worst-case execution time (i.e., an execution overrun occurs), it is suspended until its next release time. Again, conceptually, this overrun job is dropped
- xExtended_TCB is used to help with maintaining a list of per-task parameters.

</pre>

<hr>

Source: <a href="https://github.com/jogarces/ics-313-text-game"><i class="large github icon "></i>jogarces/ics-313-text-game</a>
