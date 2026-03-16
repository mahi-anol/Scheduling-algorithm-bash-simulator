# CPU Scheduling Algorithm Simulator

A Bash-based interactive simulator for three classic CPU scheduling algorithms. Built as a terminal application, it accepts process parameters, computes all key timing metrics, and renders both a formatted results table and a Gantt chart — all in the shell.

---

## Features

- Simulates **FCFS**, **SJF (non-preemptive)**, and **Priority Scheduling (non-preemptive)**
- Calculates Completion Time (CT), Waiting Time (WT), Turnaround Time (TAT), and Response Time (RT)
- Displays a formatted bordered process table for both input and output
- Renders an ASCII Gantt chart after each simulation
- Shows average TAT and CT across all processes
- Interactive menu — run multiple simulations without restarting

---

## Requirements

- A Unix-like OS: Linux, macOS, or WSL on Windows
- **Bash 4.0 or higher** (uses associative arrays and arithmetic features)

To check your Bash version:

```bash
bash --version
```

---

## Getting Started

**1. Clone or download the script**

```bash
git clone https://github.com/your-username/cpu-scheduling-simulator.git
cd cpu-scheduling-simulator
```

**2. Make the script executable**

```bash
chmod +x scheduler.sh
```

**3. Run it**

```bash
./scheduler.sh
```

---

## Usage

When you launch the script, you'll see a welcome menu:

```
*********Welcome to CPU Scheduling Algorithm Simulator*********

Please Select an algorithm you want to simulate:
1) First Come First Serve (FCFS)
2) Shortest Job First (SJF)
3) Priority Scheduling Non-Preemptive
4) Exit
```

Enter the number for the algorithm you want to simulate. You'll then be prompted to enter the number of processes, followed by the details for each one.

**Example input for FCFS (3 processes):**

```
Enter Number of processes: 3
Enter process id, arrival time, burst time for process 1: 1 0 5
Enter process id, arrival time, burst time for process 2: 2 1 3
Enter process id, arrival time, burst time for process 3: 3 2 8
```

**Example output:**

```
|Process ID      |Arrival Time    |Burst Time      |completion time |waiting time    |Turn around time|Response time   |
|1               |0               |5               |5               |0               |5               |0               |
|2               |1               |3               |8               |4               |7               |4               |
|3               |2               |8               |16              |6               |14              |6               |

Total avg turn around time = 8
Total avg completion time = 9

x-x-x-x-x-x-x-Grant chart-x-x-x-x-x-x-x-x-x
 ---------- ------  ----------------
|    p1     |  p2 |       p3       |
 ---------- ------ ----------------
0          5      8               16
```

---

## Algorithms Explained

**First Come First Serve (FCFS)** — Processes are served in order of their arrival time. Simple and fair, but can lead to the convoy effect when a long process blocks shorter ones behind it.

**Shortest Job First (SJF)** — Among the processes available at a given time, the one with the shortest burst time is selected next. Minimises average waiting time but requires knowledge of burst times in advance.

**Priority Scheduling (Non-Preemptive)** — Each process is given a priority value. The scheduler runs the highest-priority available process to completion before picking the next. Ties in priority or arrival time are broken by process ID.

---

## Input Fields Reference

| Field | Description |
|---|---|
| Process ID | A numeric identifier for the process |
| Arrival Time | The time at which the process enters the ready queue |
| Burst Time | The total CPU time the process requires |
| Priority | (Priority scheduling only) Lower value = higher priority |

---

## Project Structure

```
scheduler.sh        # Main script containing all logic and the entry point
```

All functions are defined and called within a single Bash script. Key functions include:

- `fcfs()`, `sjf()`, `npps()` — algorithm entry points
- `sorta()`, `sortb()`, `sortp()` — sorting utilities
- `WaitingTime()`, `TurnAroundTime()`, `CompletionTime()`, `ResponceTime()` — metric calculations
- `print_output()`, `draw_grant()` — result rendering

---

## Known Limitations

- All arithmetic uses integer math — fractional burst or arrival times are not supported
- The Gantt chart rendering assumes sequential, non-preemptive execution
- No preemptive algorithms (Round Robin, Preemptive SJF) are currently included
- The `tat[$val]=${pid[$i]}` line in `calc_times_sjf()` is a known typo in the original source — it assigns a PID to a TAT slot, which may produce incorrect TAT values for reordered processes in SJF

---

## Developed By

| Student ID | Name |
|---|---|
| 201-15-13664 | Mahi Sarwar Anol |
| 201-15-14046 | Fabia Chowdhury |
| 201-15-13735 | Jannat Ara Haque Jui |

---

## License

This project was developed for academic purposes. Feel free to use and extend it with attribution.
