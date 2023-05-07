---
layout: project
type: project
image: img/cotton/FreeRTOS_logo.jpeg
title: "Implementation of Overload Scheduling Algorithms in FreeRTOS"
date: 2023
published: true
labels:
  - RTOS
  - C
summary: "Implementation of Rate Monotonic Scheduling and Deadline Monotonic Scheduling Algorithms in FreeRTOS"
---

<img class="img-fluid" src="../img/cotton/freertos.png">

Designed a custom scheduler to implement the RMS and DMS (pre-emptive) scheduling algorithm in C based on FreeRTOS.

The summary of the algorithms and implementation is as follows:

<h3> Rate Monotonic Scheduling </h3>
RMS is a priority-based scheduling algorithm used to schedule periodic real-time tasks. It assigns priorities to tasks based on their periods, with shorter periods assigned higher priorities. The fundamental principle of RMS is that tasks with shorter periods have higher priority and are scheduled before tasks with longer periods. This algorithm assumes that the execution times of tasks are known and constant.

Key features of RMS:
- Priority assignment based on task periods.
- Fixed-priority scheduling.
- Assumes deterministic task execution times.
- Preemptive scheduling (higher priority tasks can preempt lower priority tasks).
- Guarantees the schedulability of a set of tasks if their total utilization is less than a certain threshold (around 69%).

<h3> Deadline Monotonic Scheduling </h3>
Deadline Monotonic Scheduling (DMS):
DMS is also a priority-based scheduling algorithm used for real-time systems. Like RMS, it assigns priorities to tasks based on their deadlines. However, unlike RMS, DMS does not assume deterministic execution times. Instead, it focuses on meeting task deadlines, considering the worst-case execution time.
Key features of DMS:

- Priority assignment based on task deadlines.
- Fixed-priority scheduling.
- Considers worst-case execution times.
- Preemptive scheduling.
- Guarantees the schedulability of a set of tasks if their total utilization is less than a certain threshold (around 100%).

<h1>Priority assignment is carried out in the following way </h1>
```cpp
static void prvSetFixedPriorities(void)
{
	BaseType_t xIter, xIndex;
	TickType_t xShortest, xPreviousShortest = 0;
	SchedTCB_t* pxShortestTaskPointer, * pxTCB;

#if (schedUSE_SCHEDULER_TASK == 1)
	BaseType_t xHighestPriority = schedSCHEDULER_PRIORITY;
#else
	BaseType_t xHighestPriority = configMAX_PRIORITIES;
#endif /* schedUSE_SCHEDULER_TASK */

	for (xIter = 0; xIter < xTaskCounter; xIter++)
	{
		xShortest = portMAX_DELAY;

		/* search for shortest period */
		for (xIndex = 0; xIndex < xTaskCounter; xIndex++)
		{
			/* your implementation goes here */
			if (xTCBArray[xIndex].xInUse == pdFALSE)
				continue;
			if (xTCBArray[xIndex].xPriorityIsSet == pdTRUE)
				continue;

		#if (schedSCHEDULING_POLICY == schedSCHEDULING_POLICY_RMS)
			/* your implementation goes here */
			if (xShortest > xTCBArray[xIndex].xPeriod)
			{
				xShortest = xTCBArray[xIndex].xPeriod;
				pxShortestTaskPointer = &xTCBArray[xIndex];
			}
		#endif /* schedSCHEDULING_POLICY */
		#if (schedSCHEDULING_POLICY == schedSCHEDULING_POLICY_DMS)
			if (xShortest > xTCBArray[xIndex].xRelativeDeadline)
			{
				xShortest = xTCBArray[xIndex].xRelativeDeadline;
				pxShortestTaskPointer = &xTCBArray[xIndex];
			}
		#endif /* schedSCHEDULING_POLICY */
		}

		/* set highest priority to task with xShortest period (the highest priority is configMAX_PRIORITIES-1) */

		/* your implementation goes here */
		if (xShortest != xPreviousShortest)
		{
			if (xHighestPriority > 0)
			{
				xHighestPriority--;
			}
			else
			{
				xHighestPriority = 0;
			}
		}
		configASSERT(0 <= xHighestPriority);
		pxShortestTaskPointer->uxPriority = xHighestPriority;
		pxShortestTaskPointer->xPriorityIsSet = pdTRUE;
		xPreviousShortest = xShortest;
	}
}
#endif /* schedSCHEDULING_POLICY */
```

- The algorithm does not perform any schedulability test.
- In the event that a job misses its deadline, it is suspended and runs as a new job at its next release time. In other words, the current (missed) instance of the task is dropped.
- The code prints out relevant information to the serial monitor, e.g., which task is executing, if a task misses its deadline, etc.
- If a job executes for more than its worst-case execution time (i.e., an execution overrun occurs), it is suspended until its next release time. Again, conceptually, this overrun job is dropped
- xExtended_TCB is used to help with maintaining a list of per-task parameters.
```cpp
typedef struct xExtended_TCB
{
	TaskFunction_t pvTaskCode;	  /* Function pointer to the code that will be run periodically. */
	const char* pcName;			  /* Name of the task. */
	UBaseType_t uxStackDepth;	  /* Stack size of the task. */
	void* pvParameters;			  /* Parameters to the task function. */
	UBaseType_t uxPriority;		  /* Priority of the task. */
	TaskHandle_t* pxTaskHandle;	  /* Task handle for the task. */
	TickType_t xReleaseTime;	  /* Release time of the task. */
	TickType_t xRelativeDeadline; /* Relative deadline of the task. */
	TickType_t xAbsoluteDeadline; /* Absolute deadline of the task. */
	TickType_t xPeriod;			  /* Task period. */
	TickType_t xLastWakeTime;	  /* Last time stamp when the task was running. */
	TickType_t xMaxExecTime;	  /* Worst-case execution time of the task. */
	TickType_t xExecTime;		  /* Current execution time of the task. */

	BaseType_t xWorkIsDone; /* pdFALSE if the job is not finished, pdTRUE if the job is finished. */
} Sched_TCB;
```



Source: <a href="https://github.com/shreyasharathi/rms-dms-scheduler"><i class="large github icon "></i>shreyasharathi/rms-dms-scheduler</a>
