# OS Laboratory 2 - CPU Scheduling Algorithms

**Course:** BCA151 Operating System
**Name:** Rabbah Alawi
**Course & Year:** BSCA - 3rd Year
**Date:** October 26, 2026

This repository contains a Python CPU Scheduling Simulator (`cpu_scheduling.py`) that implements FCFS, non-preemptive SJF, non-preemptive Priority, Round Robin, and SRTF.

Formulas used: **TAT = CT − AT**, **WT = TAT − BT**, **RT = First CPU Start − AT**

---

## Datasets

**Original dataset** (FCFS, SJF, Priority, Round Robin with time quantum = 2 ms):

| Process | Arrival Time | Burst Time | Priority |
|---|---|---|---|
| P1 | 0 | 8 | 2 |
| P2 | 0 | 4 | 1 |
| P3 | 0 | 2 | 4 |
| P4 | 0 | 6 | 3 |

**Modified dataset** (same data used for FCFS, SJF, Priority, and Round Robin):

| Process | Arrival Time | Burst Time | Priority |
|---|---|---|---|
| P1 | 0 | 5 | 1 |
| P2 | 0 | 7 | 3 |
| P3 | 0 | 6 | 2 |
| P4 | 0 | 8 | 4 |

**SRTF dataset** (separate dataset, used in both parts):

| Process | Arrival Time | Burst Time | Priority |
|---|---|---|---|
| P1 | 0 | 8 | 2 |
| P2 | 1 | 4 | 1 |
| P3 | 2 | 2 | 4 |
| P4 | 3 | 1 | 3 |

---

# Part 1: Original Dataset Results

## Gantt Charts

**1. FCFS**
```
|       P1      |   P2  | P3|     P4    |
0               8       12  14          20
```

**2. Non-Preemptive SJF**
```
| P3|   P2  |     P4    |       P1      |
0   2       6           12              20
```

**3. Non-Preemptive Priority**
```
|   P2  |       P1      |     P4    | P3|
0       4               12          18  20
```

**4. Round Robin (q = 2)**
```
| P1| P2| P3| P4| P1| P2| P4| P1| P4| P1|
0   2   4   6   8   10  12  14  16  18  20
```

**5. SRTF (separate dataset)**
```
|P1|P2|  P3 |P4|   P2   |         P1         |
0  1  2     4  5        8                    15
```

## Calculation Tables

### FCFS

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 8 | 8 | 0 | 0 |
| P2 | 0 | 4 | 12 | 12 | 8 | 8 |
| P3 | 0 | 2 | 14 | 14 | 12 | 12 |
| P4 | 0 | 6 | 20 | 20 | 14 | 14 |
| **Average** | | | | **13.50** | **8.50** | **8.50** |

### Non-Preemptive SJF

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 20 | 20 | 12 | 12 |
| P2 | 0 | 4 | 6 | 6 | 2 | 2 |
| P3 | 0 | 2 | 2 | 2 | 0 | 0 |
| P4 | 0 | 6 | 12 | 12 | 6 | 6 |
| **Average** | | | | **10.00** | **5.00** | **5.00** |

### Non-Preemptive Priority

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 12 | 12 | 4 | 4 |
| P2 | 0 | 4 | 4 | 4 | 0 | 0 |
| P3 | 0 | 2 | 20 | 20 | 18 | 18 |
| P4 | 0 | 6 | 18 | 18 | 12 | 12 |
| **Average** | | | | **13.50** | **8.50** | **8.50** |

### Round Robin (q = 2)

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 20 | 20 | 12 | 0 |
| P2 | 0 | 4 | 12 | 12 | 8 | 2 |
| P3 | 0 | 2 | 6 | 6 | 4 | 4 |
| P4 | 0 | 6 | 18 | 18 | 12 | 6 |
| **Average** | | | | **14.00** | **9.00** | **3.00** |

### SRTF (separate dataset)

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 15 | 15 | 7 | 0 |
| P2 | 1 | 4 | 8 | 7 | 3 | 0 |
| P3 | 2 | 2 | 4 | 2 | 0 | 0 |
| P4 | 3 | 1 | 5 | 2 | 1 | 1 |
| **Average** | | | | **6.50** | **2.75** | **0.25** |

## Comparison Table of Averages (Original Dataset)

| Algorithm | Average WT | Average TAT | Average RT |
|---|---|---|---|
| FCFS | 8.50 ms | 13.50 ms | 8.50 ms |
| Non-Preemptive SJF | 5.00 ms | 10.00 ms | 5.00 ms |
| Non-Preemptive Priority | 8.50 ms | 13.50 ms | 8.50 ms |
| Round Robin (q = 2) | 9.00 ms | 14.00 ms | 3.00 ms |
| SRTF* | 2.75 ms | 6.50 ms | 0.25 ms |

\*SRTF used a separate dataset with different arrival times, so it is not directly comparable to the other four.

## Round Robin Time Quantum Experiment

Original dataset (P1 = 8, P2 = 4, P3 = 2, P4 = 6; all arrive at 0):

| Time Quantum | Average WT | Average TAT | Average RT | CPU Allocations |
|---|---|---|---|---|
| 1 ms | 9.50 ms | 14.50 ms | 1.50 ms | 20 |
| 2 ms | 9.00 ms | 14.00 ms | 3.00 ms | 10 |
| 4 ms | 9.00 ms | 14.00 ms | 5.50 ms | 6 |

_Note: for q = 1, the program's Gantt chart merges consecutive 1 ms turns of the same process (P1 at 18-20), but there are still 20 one-millisecond allocations in total._

**Observations:**
- A smaller quantum means more CPU allocations (more context switches).
- Average waiting time was lowest at q = 2 and q = 4 (9.00 ms) in these tests.
- A larger quantum gives a slower first response (RT 5.50 ms at q = 4).
- A very large quantum makes Round Robin behave like FCFS.

---

# Part 2: Modified Dataset Results

Burst times and priorities were changed in `PROCESSES`:

```python
PROCESSES = [
    {"pid": "P1", "at": 0, "bt": 5, "priority": 1},
    {"pid": "P2", "at": 0, "bt": 7, "priority": 3},
    {"pid": "P3", "at": 0, "bt": 6, "priority": 2},
    {"pid": "P4", "at": 0, "bt": 8, "priority": 4},
]
```

The Round Robin quantum was kept at 2 ms. `SRTF_PROCESSES` was not changed.

## Gantt Charts (Modified Dataset)

**1. FCFS**
```
|    P1   |      P2     |     P3    |       P4      |
0         5             12          18              26
```

**2. Non-Preemptive SJF**
```
|    P1   |     P3    |      P2     |       P4      |
0         5           11            18              26
```

**3. Non-Preemptive Priority**
```
|    P1   |     P3    |      P2     |       P4      |
0         5           11            18              26
```

**4. Round Robin (q = 2)**
```
|  P1 |  P2 |  P3 |  P4 |  P1 |  P2 |  P3 |  P4 |P1|  P2 |  P3 |  P4 |P2|  P4 |
0     2     4     6     8     10    12    14    16 17    19    21    23 24    26
```

**5. SRTF** uses the separate dataset, so its Gantt chart is the same as in Part 1.

## Calculation Tables (Modified Dataset)

### FCFS

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 5 | 5 | 5 | 0 | 0 |
| P2 | 0 | 7 | 12 | 12 | 5 | 5 |
| P3 | 0 | 6 | 18 | 18 | 12 | 12 |
| P4 | 0 | 8 | 26 | 26 | 18 | 18 |
| **Average** | | | | **15.25** | **8.75** | **8.75** |

### Non-Preemptive SJF

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 5 | 5 | 5 | 0 | 0 |
| P2 | 0 | 7 | 18 | 18 | 11 | 11 |
| P3 | 0 | 6 | 11 | 11 | 5 | 5 |
| P4 | 0 | 8 | 26 | 26 | 18 | 18 |
| **Average** | | | | **15.00** | **8.50** | **8.50** |

### Non-Preemptive Priority

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 5 | 5 | 5 | 0 | 0 |
| P2 | 0 | 7 | 18 | 18 | 11 | 11 |
| P3 | 0 | 6 | 11 | 11 | 5 | 5 |
| P4 | 0 | 8 | 26 | 26 | 18 | 18 |
| **Average** | | | | **15.00** | **8.50** | **8.50** |

### Round Robin (q = 2)

| Process | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 5 | 17 | 17 | 12 | 0 |
| P2 | 0 | 7 | 24 | 24 | 17 | 2 |
| P3 | 0 | 6 | 21 | 21 | 15 | 4 |
| P4 | 0 | 8 | 26 | 26 | 18 | 6 |
| **Average** | | | | **22.00** | **15.50** | **3.00** |

### SRTF

Same as Part 1 (separate dataset): Average WT = 2.75 ms, Average TAT = 6.50 ms, Average RT = 0.25 ms.

## Comparison Table (Modified Dataset)

| Algorithm | Average WT | Average TAT | Average RT |
|---|---|---|---|
| FCFS | 8.75 ms | 15.25 ms | 8.75 ms |
| SJF | 8.50 ms | 15.00 ms | 8.50 ms |
| Priority | 8.50 ms | 15.00 ms | 8.50 ms |
| Round Robin (q = 2) | 15.50 ms | 22.00 ms | 3.00 ms |
| SRTF* | 2.75 ms | 6.50 ms | 0.25 ms |

\*SRTF used the separate dataset with different arrival times.

**Observations:**
- SJF and Priority gave identical results because in the modified dataset, the order of shortest burst time (P1, P3, P2, P4) is the same as the order of highest priority (P1, P3, P2, P4).
- SJF and Priority had the lowest average waiting time (8.50 ms), but only slightly lower than FCFS (8.75 ms), because the burst times are close to each other (5 to 8 ms), so the processes' order matters less.
- Round Robin had a much higher average waiting time (15.50 ms) because all processes have similar burst times, so each one is repeatedly interrupted and finishes late. However, it kept the lowest response time of the four (3.00 ms).

---

# Answers to the Questions

1. **CPU Scheduling:** It is how the operating system chooses which process will use the CPU next. It is needed because many processes need the CPU.

2. **FCFS vs. SJF:** FCFS runs processes in arrival order, while SJF runs the process with the shortest burst time first.

3. **Why SJF has lower waiting time:** Short processes finish faster, so other processes do not need to wait too long.

4. **Priority Scheduling:** It runs the process with the highest priority. In our activity, the smallest priority number means the highest priority.

5. **Starvation:** It happens when a process waits for a very long time because other processes keep running first.

6. **Round Robin Responsiveness:** Each process gets a turn to use the CPU. This helps processes respond faster, with an average response time of 3.00 ms in our experiment.

7. **Effect of Time Quantum:** A smaller quantum gives processes faster turns but causes more CPU switches. A larger quantum reduces switches but may make processes wait longer for their first turn.

8. **SRTF vs. SJF:** SRTF can interrupt a running process if a shorter process arrives. Non-preemptive SJF does not interrupt a running process.

9. **Context Saving:** The operating system saves a process's current state when it is interrupted so it can continue later.

10. **Is the Lowest Waiting Time Always Best?** No. Some processes may wait too long, and interactive systems need fast responses, not just low waiting times.

11. **Why Use the Same Dataset?** It makes the comparison fair because all algorithms use the same processes and values.

12. **GitHub's Role:** GitHub helps us save our code, track changes, keep a backup, and submit our laboratory work.

---

# Conclusion

In this laboratory activity, we implemented five CPU scheduling algorithms: FCFS, non-preemptive SJF, non-preemptive Priority, Round Robin, and SRTF using Python in GitHub Codespaces. We created Gantt charts and calculated the process times. We also checked the results manually using the formulas TAT = CT − AT, WT = TAT − BT, and RT = first start − AT.

Based on the same dataset, non-preemptive SJF had the lowest average waiting time of 5.00 ms and turnaround time of 10.00 ms because it runs shorter processes first. FCFS and Priority Scheduling both had an average waiting time of 8.50 ms. FCFS is easy to use, but a long process at the beginning can make other processes wait longer. Priority Scheduling follows the assigned priorities, but low-priority processes like P3 may wait for a long time. Round Robin had the highest average waiting time of 9.00 ms but the lowest average response time among the four algorithms at 3.00 ms. This makes it useful for systems where users need quick responses. SRTF was tested using a different dataset. It allowed shorter processes to interrupt longer ones, giving an average waiting time of 2.75 ms. However, long processes may wait too long, and frequent interruptions can add overhead.

In the Round Robin experiment, we learned that the time quantum affects performance. A smaller quantum of 1 ms improved the response time to 1.50 ms but increased CPU allocations and average waiting time to 9.50 ms. A larger quantum of 4 ms reduced the number of switches but increased the response time to 5.50 ms. If the quantum is too large, Round Robin works almost like FCFS.

When we changed the burst times and priorities in the modified dataset, the results showed that the dataset affects how different the algorithms perform. SJF and Priority gave the same schedule because the shortest processes also had the highest priority, and the gap between FCFS (8.75 ms) and SJF (8.50 ms) became small because the burst times were close to each other. Round Robin's average waiting time rose to 15.50 ms, but it still gave the lowest response time of 3.00 ms among the four algorithms.

Overall, we learned that each algorithm has its own advantages and disadvantages. SJF and SRTF help reduce waiting time, while Round Robin is better for quick responses. There is no single best algorithm for every situation. We also learned that GitHub is useful for saving, managing, and submitting our laboratory work.
