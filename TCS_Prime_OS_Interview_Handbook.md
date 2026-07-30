# TCS Prime Operating Systems — Interview Handbook

### Prepared for: TCS Prime | TCS Digital | TCS Ninja Technical Interviews
### 100 Most Important OS Questions + Bonus "Top 30 TCS Favorites"

---

## How to Use This Handbook

- Answers are written **exactly the way you should say them in an interview** — short, confident, and technically correct.
- Each answer is capped at **4–5 lines** so it's easy to revise the night before your interview.
- Topics are arranged in the **exact order interviewers usually build up questions** — from basics to advanced, with comparisons and scenarios woven in.
- The final section, **⭐ Top 30 TCS Favorites**, is your last-minute rapid-fire revision list.

---

## Table of Contents

| S.No | Topic | No. of Questions | Difficulty |
|------|-------|:---:|:---:|
| 1 | Introduction to Operating Systems | 4 | Easy |
| 2 | OS Architecture & Components | 5 | Easy |
| 3 | Processes | 6 | Easy |
| 4 | Threads | 5 | Medium |
| 5 | CPU Scheduling | 8 | Medium |
| 6 | Process Synchronization | 7 | Medium |
| 7 | Deadlocks | 5 | Hard |
| 8 | Memory Management | 6 | Medium |
| 9 | Virtual Memory | 5 | Hard |
| 10 | Page Replacement Algorithms | 5 | Hard |
| 11 | File Systems | 4 | Medium |
| 12 | Disk Scheduling | 5 | Hard |
| 13 | System Calls & Interrupts | 4 | Medium |
| 14 | I/O Management | 4 | Medium |
| 15 | Protection & Security | 4 | Hard |
| 16 | Multiprocessing & Parallelism | 4 | Medium |
| 17 | Linux & Windows Basics | 4 | Medium |
| 18 | Miscellaneous Important Concepts | 5 | Medium |
| 19 | Scenario-Based Questions | 10 | Hard |
| **—** | **Core Handbook Total** | **100** | **Mixed** |
| ⭐ | Bonus: Top 30 TCS Favorites (Quick Revision) | 30 | Mixed |

---
---

## Topic 1: Introduction to Operating Systems
**Difficulty: Easy**

### Question 1
**Topic:** Introduction to Operating Systems | **Difficulty:** Easy

**Q: What is an Operating System?**

**A:**
- OS is system software that acts as an interface between the user and computer hardware.
- It manages hardware resources like CPU, memory, storage, and I/O devices.
- It provides a platform on which application programs can run.
- Examples: Windows, Linux, macOS, Android.

---

### Question 2
**Topic:** Introduction to Operating Systems | **Difficulty:** Easy

**Q: What are the main goals and functions of an Operating System?**

**A:**
- Two main goals: **convenience** for the user and **efficient use** of hardware.
- Key functions: process management, memory management, file management, device management, and security.
- It provides abstraction — hiding hardware complexity from applications.
- It also enables multitasking, so multiple programs can run without interfering with each other.

---

### Question 3
**Topic:** Introduction to Operating Systems | **Difficulty:** Easy

**Q: Why do we need an Operating System? What would happen without one?**

**A:**
- Without an OS, every application would need to directly control hardware — complex and error-prone.
- OS provides resource sharing, scheduling, and protection between programs.
- It ensures fair CPU allocation and prevents one process from corrupting another's memory.
- It also handles error detection, security, and a consistent user interface.

---

### Question 4
**Topic:** Introduction to Operating Systems | **Difficulty:** Easy

**Q: What are the different types of Operating Systems?**

**A:**
- **Batch OS** — executes jobs in batches with no user interaction.
- **Time-Sharing OS** — multiple users share CPU time via quick switching (e.g., Linux servers).
- **Distributed OS** — manages a group of independent computers as a single system.
- **Real-Time OS** — guarantees response within a strict time limit (e.g., pacemakers, industrial control).

---
---

## Topic 2: OS Architecture & Components
**Difficulty: Easy**

### Question 5
**Topic:** OS Architecture & Components | **Difficulty:** Easy

**Q: What is a Kernel?**

**A:**
- Kernel is the core part of the OS that directly interacts with hardware.
- It manages CPU scheduling, memory, and device operations at the lowest level.
- It runs in kernel mode with unrestricted access to hardware.
- Examples: Linux kernel, Windows NT kernel.

---

### Question 6
**Topic:** OS Architecture & Components | **Difficulty:** Easy

**Q: What is the difference between Kernel and Shell?**

**A:**
- Kernel is the core that manages hardware resources directly and runs in kernel mode.
- Shell is the interface between the user and the kernel — it interprets user commands.
- Shell can be CLI-based (like bash) or GUI-based.
- User commands go through the shell, which then requests services from the kernel.

---

### Question 7
**Topic:** OS Architecture & Components | **Difficulty:** Medium

**Q: What is the difference between Monolithic Kernel and Microkernel?**

**A:**
- Monolithic kernel runs all OS services (drivers, file system, memory management) in one kernel space — fast but less stable; a bug in any service can crash the system.
- Microkernel keeps only essential services (IPC, basic scheduling) in kernel space; everything else runs in user space — more stable and modular, but slightly slower due to extra context switches.
- Linux uses a monolithic kernel; QNX and Minix use microkernels.
- Hybrid kernels (Windows, macOS) combine both approaches for a balance of speed and modularity.

---

### Question 8
**Topic:** OS Architecture & Components | **Difficulty:** Medium

**Q: What is the difference between User Mode and Kernel Mode?**

**A:**
- User mode is a restricted mode where applications run with limited hardware access.
- Kernel mode has full, unrestricted access to hardware and system resources.
- The CPU switches from user mode to kernel mode via a system call or interrupt.
- This separation protects the system from crashing due to faulty or malicious user programs.

---

### Question 9
**Topic:** OS Architecture & Components | **Difficulty:** Easy

**Q: Explain the Booting Process, and the difference between BIOS and UEFI.**

**A:**
- Booting is the process of starting up a computer and loading the OS into memory.
- Firmware (BIOS/UEFI) first runs POST (Power-On Self-Test), then loads the bootloader, which loads the kernel.
- BIOS is older, 16-bit, uses MBR partitioning, and boots slower.
- UEFI is modern, supports GPT, boots faster, and adds security features like Secure Boot.

---
---

## Topic 3: Processes
**Difficulty: Easy**

### Question 10
**Topic:** Processes | **Difficulty:** Easy

**Q: What is a Process?**

**A:**
- A process is a program in execution, along with its current activity.
- It's an active entity, unlike a program which is just passive instructions on disk.
- Each process has its own memory space, registers, and a Process Control Block (PCB).
- Example: opening two Chrome windows creates two separate processes.

---

### Question 11
**Topic:** Processes | **Difficulty:** Easy

**Q: What is the difference between a Program and a Process?**

**A:**
- A program is a passive, static set of instructions stored on disk.
- A process is an active, dynamic instance of a program that is currently executing.
- A single program can be run multiple times, creating multiple separate processes.
- A process needs resources like CPU, memory, and I/O; a program does not.

---

### Question 12
**Topic:** Processes | **Difficulty:** Easy

**Q: Explain Process States with the state diagram.**

**A:**
- A process moves through **New → Ready → Running → Waiting → Terminated**.
- **New:** process is being created. **Ready:** waiting in queue for CPU.
- **Running:** currently executing on the CPU. **Waiting/Blocked:** waiting for I/O or an event.
- **Terminated:** execution has finished and resources are released.

---

### Question 13
**Topic:** Processes | **Difficulty:** Easy

**Q: What is a Process Control Block (PCB)?**

**A:**
- PCB is a data structure the OS maintains for every process.
- It stores process ID, state, program counter, CPU registers, memory limits, and I/O status.
- The OS uses the PCB during context switching to save and restore process state.
- It's essentially the "identity card" of a process.

---

### Question 14
**Topic:** Processes | **Difficulty:** Medium

**Q: What is Context Switching, and why does it have overhead?**

**A:**
- Context switching is saving the state of the current process and loading the state of the next process to run.
- It happens during scheduling, interrupts, or system calls.
- It has overhead because no useful work happens during the switch — pure time is spent saving/restoring registers and memory maps.
- Frequent context switching (e.g., a very small time quantum) can noticeably reduce system throughput.

---

### Question 15
**Topic:** Processes | **Difficulty:** Easy

**Q: What are Zombie, Orphan, and Daemon processes?**

**A:**
- **Zombie process** has finished execution but still has an entry in the process table because its parent hasn't read its exit status.
- **Orphan process** is one whose parent has terminated before it; it gets adopted by the init/systemd process.
- **Daemon process** runs continuously in the background providing a service (e.g., cron, sshd).
- Daemons usually start at boot and have no controlling terminal.

---

## Topic 4: Threads
**Difficulty: Medium**

### Question 16
**Topic:** Threads | **Difficulty:** Easy

**Q: What is a Thread?**

**A:**
- A thread is the smallest unit of execution within a process, sharing the process's memory and resources.
- Multiple threads within a process can run concurrently.
- Each thread has its own stack, register set, and program counter.
- Example: a browser tab rendering a page while downloading a file, in separate threads.

---

### Question 17
**Topic:** Threads | **Difficulty:** Medium

**Q: What is the difference between Process and Thread?**

**A:**
- A process has its own independent memory space; threads share memory within the same process.
- Process creation is heavyweight (more overhead); thread creation is lightweight and faster.
- Inter-process communication is costlier than inter-thread communication.
- A crash in one process doesn't affect others, but a crash in one thread can bring down the whole process.

---

### Question 18
**Topic:** Threads | **Difficulty:** Medium

**Q: What is the difference between User-Level Threads and Kernel-Level Threads?**

**A:**
- User-level threads are managed by a library in user space without kernel involvement — very fast context switching, but a blocking call blocks the entire process.
- Kernel-level threads are created and scheduled directly by the OS kernel — slower to switch, but they enable true parallelism on multicore CPUs.
- Java and most modern OS use kernel-level (native) threads.
- Many systems use a hybrid model combining both for flexibility.

---

### Question 19
**Topic:** Threads | **Difficulty:** Medium

**Q: What is Multithreading, and what are its advantages?**

**A:**
- Multithreading means running multiple threads within a single process concurrently.
- Advantages: better CPU utilization, faster execution through parallelism, and improved responsiveness.
- Threads share memory, so resource sharing is efficient compared to separate processes.
- Example: a word processor spell-checking in the background while the user keeps typing.

---

### Question 20
**Topic:** Threads | **Difficulty:** Easy

**Q: Explain the Thread Life Cycle.**

**A:**
- A thread moves through **New → Runnable → Running → Blocked/Waiting → Terminated**.
- **New:** thread object created but not yet started.
- **Runnable:** ready to run, waiting for CPU. **Running:** actively executing.
- **Blocked:** waiting for I/O, a lock, or a signal. **Terminated:** execution complete.

---
---

## Topic 5: CPU Scheduling
**Difficulty: Medium**

### Question 21
**Topic:** CPU Scheduling | **Difficulty:** Easy

**Q: What is the difference between the CPU Scheduler and the Dispatcher?**

**A:**
- The CPU Scheduler selects which process from the ready queue should run next, based on a scheduling algorithm.
- The Dispatcher actually performs the context switch and hands CPU control to the selected process.
- In short: scheduler decides "who," dispatcher does "how."
- Dispatcher latency is the time taken to stop one process and start another.

---

### Question 22
**Topic:** CPU Scheduling | **Difficulty:** Medium

**Q: What are the main CPU Scheduling Criteria?**

**A:**
- **CPU Utilization** — keep the CPU as busy as possible.
- **Throughput** — number of processes completed per unit time.
- **Turnaround Time** — total time from submission to completion.
- **Waiting Time** and **Response Time** — time in ready queue, and time to first output, respectively.

---

### Question 23
**Topic:** CPU Scheduling | **Difficulty:** Medium

**Q: What is the difference between Preemptive and Non-preemptive Scheduling?**

**A:**
- In preemptive scheduling, the OS can forcibly take the CPU away from a running process (e.g., Round Robin, SRTF).
- In non-preemptive scheduling, a process holds the CPU until it finishes or voluntarily yields (e.g., FCFS, non-preemptive SJF).
- Preemptive gives better responsiveness but has higher context-switch overhead.
- Non-preemptive is simpler but can delay short jobs behind long-running ones.

---

### Question 24
**Topic:** CPU Scheduling | **Difficulty:** Easy

**Q: Explain FCFS Scheduling. What is its major drawback?**

**A:**
- First Come First Serve executes processes strictly in order of arrival, like a queue.
- It is simple, non-preemptive, and fair in terms of arrival order.
- Major drawback is the **Convoy Effect** — a long process blocks all shorter processes behind it.
- This increases the average waiting time significantly.

---

### Question 25
**Topic:** CPU Scheduling | **Difficulty:** Medium

**Q: What is the difference between SJF and SRTF?**

**A:**
- SJF (Shortest Job First) selects the process with the smallest total burst time; it can be preemptive or non-preemptive.
- SRTF (Shortest Remaining Time First) is the preemptive version — it interrupts a running process if a new process arrives with a shorter remaining time.
- SRTF gives lower average waiting time but has higher context-switch overhead.
- Both can cause starvation for long processes if short jobs keep arriving.

---

### Question 26
**Topic:** CPU Scheduling | **Difficulty:** Medium

**Q: What is Priority Scheduling, and what problem does it cause?**

**A:**
- Each process is assigned a priority, and the CPU is given to the highest-priority process first.
- It can be implemented as preemptive or non-preemptive.
- Problem: low-priority processes may **starve** if high-priority processes keep arriving.
- Solution: **Aging** — gradually increasing the priority of processes that wait too long.

---

### Question 27
**Topic:** CPU Scheduling | **Difficulty:** Medium

**Q: Explain Round Robin Scheduling. Why is it preferred in time-sharing systems?**

**A:**
- Each process gets a fixed time slice (quantum) in cyclic order; if not finished, it goes to the back of the queue.
- It is preemptive and gives every process a fair share of CPU time.
- It's preferred in time-sharing systems because it ensures good response time for interactive users.
- Choosing the right quantum matters — too small causes excessive switching, too large behaves like FCFS.

---

### Question 28
**Topic:** CPU Scheduling | **Difficulty:** Hard

**Q: What is the difference between Multilevel Queue and Multilevel Feedback Queue Scheduling?**

**A:**
- Multilevel Queue divides the ready queue into fixed categories (system, interactive, batch), each with its own algorithm — processes never move between queues.
- Multilevel Feedback Queue allows processes to move between queues based on behavior and aging.
- MFQ is more flexible and prevents starvation better, but is more complex to implement.
- MLQ is simpler and predictable, but rigid once a process is assigned to a queue.

---
---

## Topic 6: Process Synchronization
**Difficulty: Medium**

### Question 29
**Topic:** Process Synchronization | **Difficulty:** Easy

**Q: What is the Critical Section Problem?**

**A:**
- The Critical Section is the part of code where a process accesses shared resources like variables or files.
- The problem is designing a protocol so that when one process is in its critical section, no other process can enter its own.
- A correct solution must guarantee **Mutual Exclusion, Progress, and Bounded Waiting**.
- It's the foundation of all synchronization mechanisms in OS.

---

### Question 30
**Topic:** Process Synchronization | **Difficulty:** Medium

**Q: What is a Race Condition?**

**A:**
- A race condition occurs when multiple processes/threads access shared data concurrently, and the final outcome depends on execution order.
- It leads to inconsistent or incorrect results.
- Example: two threads incrementing a shared counter simultaneously can lose an update.
- It's prevented using synchronization tools like locks, mutexes, or semaphores.

---

### Question 31
**Topic:** Process Synchronization | **Difficulty:** Easy

**Q: What is Mutual Exclusion?**

**A:**
- Mutual exclusion ensures that only one process/thread can access a critical section at a time.
- It prevents race conditions and data corruption on shared resources.
- It's implemented using locks, semaphores, or mutexes.
- Example: only one thread can write to a shared file at once.

---

### Question 32
**Topic:** Process Synchronization | **Difficulty:** Medium

**Q: What is the difference between Mutex and Semaphore?**

**A:**
- A Mutex is a locking mechanism allowing only one thread to access a resource, and only the thread that locked it can unlock it (ownership concept).
- A Semaphore is a signaling mechanism using a counter — a counting semaphore allows multiple threads limited access; a binary semaphore behaves like a lock.
- Semaphores can synchronize across different processes; mutexes are mainly for mutual exclusion within a process.
- Any thread can signal a semaphore, but only the owner can release a mutex.

---

### Question 33
**Topic:** Process Synchronization | **Difficulty:** Medium

**Q: What is a Monitor in process synchronization?**

**A:**
- A Monitor is a high-level construct that bundles shared data with the procedures that operate on it.
- It automatically ensures only one process executes inside at a time — unlike semaphores, which need manual handling.
- It uses condition variables (wait/signal) for process cooperation.
- Java's `synchronized` keyword is based on this concept.

---

### Question 34
**Topic:** Process Synchronization | **Difficulty:** Hard

**Q: What is a Spinlock, and how is it different from a Mutex?**

**A:**
- A Spinlock is a lock where the waiting thread continuously checks ("busy-waits") if the lock is free, instead of sleeping.
- It avoids context-switch overhead, making it efficient for very short critical sections on multiprocessor systems.
- A Mutex puts the waiting thread to sleep, freeing the CPU for other work — better for longer waits.
- Spinlocks waste CPU cycles if the lock is held for too long.

---

### Question 35
**Topic:** Process Synchronization | **Difficulty:** Hard

**Q: Explain the Producer-Consumer Problem.**

**A:**
- It involves a producer generating data into a shared bounded buffer, and a consumer removing data from it.
- The challenge is to synchronize so the producer never adds to a full buffer and the consumer never removes from an empty buffer.
- It's solved using three semaphores: `full`, `empty`, and `mutex`.
- It's a classic example used in real systems like message queues.

---

## Topic 7: Deadlocks
**Difficulty: Hard**

### Question 36
**Topic:** Deadlocks | **Difficulty:** Easy

**Q: What is a Deadlock? Explain with a real-life example.**

**A:**
- A deadlock is a situation where a set of processes are blocked because each is waiting for a resource held by another in the same set.
- None of them can proceed, and the system reaches a permanent standstill.
- Real-life example: at a four-way traffic jam, each car blocks the path the next one needs — nobody moves.
- It occurs only when all four necessary conditions hold simultaneously.

---

### Question 37
**Topic:** Deadlocks | **Difficulty:** Medium

**Q: What are the necessary conditions for Deadlock?**

**A:**
- **Mutual Exclusion** — a resource is held by only one process at a time.
- **Hold and Wait** — a process holds resources while waiting for more.
- **No Preemption** — resources can't be forcibly taken away.
- **Circular Wait** — a closed chain of processes, each waiting for the next. All four must hold together.

---

### Question 38
**Topic:** Deadlocks | **Difficulty:** Medium

**Q: What is a Resource Allocation Graph (RAG)?**

**A:**
- RAG is a graphical representation showing processes and resources as nodes.
- A request edge points from process to resource; an allocation edge points from resource to process.
- If the graph has a cycle and resources have a single instance each, a deadlock definitely exists.
- With multi-instance resources, a cycle doesn't always mean deadlock.

---

### Question 39
**Topic:** Deadlocks | **Difficulty:** Hard

**Q: What is the difference between Deadlock Prevention and Deadlock Avoidance?**

**A:**
- Prevention eliminates one of the four necessary conditions so deadlock can never occur (e.g., disallowing hold-and-wait).
- Avoidance allows all conditions but carefully allocates resources by checking if the resulting state stays "safe" (e.g., Banker's Algorithm).
- Prevention is more restrictive and can reduce resource utilization.
- Avoidance requires advance knowledge of each process's maximum resource needs.

---

### Question 40
**Topic:** Deadlocks | **Difficulty:** Hard

**Q: Explain the Banker's Algorithm, and Deadlock Detection/Recovery.**

**A:**
- Banker's Algorithm grants a resource request only if the resulting state is "safe" — meaning a sequence exists in which all processes can finish.
- It requires processes to declare their maximum resource needs in advance.
- Deadlock Detection periodically checks for cycles/unsafe states, without any prevention beforehand.
- Recovery is done by killing one or more processes, or preempting resources to break the cycle.

---
---

## Topic 8: Memory Management
**Difficulty: Medium**

### Question 41
**Topic:** Memory Management | **Difficulty:** Easy

**Q: What is Memory Management, and what is the difference between Logical and Physical Address?**

**A:**
- Memory management is the OS function that handles allocation, tracking, and protection of main memory.
- Logical address is generated by the CPU during program execution (relative address, used by the process).
- Physical address is the actual location in RAM, obtained after mapping.
- The Memory Management Unit (MMU) translates logical to physical addresses at runtime.

---

### Question 42
**Topic:** Memory Management | **Difficulty:** Medium

**Q: What is Address Binding?**

**A:**
- Address binding is mapping program instructions/data from logical to physical addresses.
- **Compile time** — addresses fixed at compile time; memory location must be known in advance.
- **Load time** — addresses assigned when the program is loaded into memory.
- **Execution/Run time** — addresses assigned during execution via the MMU; most flexible, used in modern systems.

---

### Question 43
**Topic:** Memory Management | **Difficulty:** Medium

**Q: What is Paging? How is it different from Segmentation?**

**A:**
- Paging divides memory into fixed-size blocks — pages (logical) and frames (physical) — which avoids external fragmentation.
- Segmentation divides memory into variable-sized logical units (code, stack, heap) based on program structure, which can cause external fragmentation.
- Paging is invisible to the programmer; segmentation reflects the logical view of a program.
- Modern systems like x86 often combine both approaches.

---

### Question 44
**Topic:** Memory Management | **Difficulty:** Medium

**Q: What is Fragmentation? Explain Internal vs External Fragmentation.**

**A:**
- Fragmentation is wasted memory that can't be effectively used.
- **Internal fragmentation** happens when allocated memory is slightly larger than requested, wasting space inside a fixed block — common in paging.
- **External fragmentation** happens when free memory is broken into small non-contiguous chunks, so no single block is big enough — common in segmentation.
- Compaction is a technique used to reduce external fragmentation.

---

### Question 45
**Topic:** Memory Management | **Difficulty:** Medium

**Q: What is Swapping?**

**A:**
- Swapping is temporarily moving a process out of main memory to secondary storage (swap space) to free up memory, and bringing it back later.
- It allows more processes to run than would otherwise fit in physical memory at once.
- It has a performance cost due to slow disk I/O compared to RAM.
- It's the foundational concept behind virtual memory techniques like demand paging.

---

### Question 46
**Topic:** Memory Management | **Difficulty:** Medium

**Q: What is Contiguous Memory Allocation?**

**A:**
- Contiguous allocation assigns each process a single continuous block of memory.
- It's simple and fast to access, using just a base and limit register.
- Drawback: leads to external fragmentation as processes are loaded and removed over time.
- Fixed partitioning causes internal fragmentation; variable partitioning causes external fragmentation.

---

## Topic 9: Virtual Memory
**Difficulty: Hard**

### Question 47
**Topic:** Virtual Memory | **Difficulty:** Medium

**Q: What is Virtual Memory? How is it different from Physical Memory?**

**A:**
- Virtual memory gives each process the illusion of a large, continuous private address space, even if physical RAM is smaller.
- Physical memory is the actual RAM installed on the machine.
- Virtual memory is implemented using paging combined with secondary storage (disk) as an overflow.
- It allows running programs larger than RAM and improves isolation between processes.

---

### Question 48
**Topic:** Virtual Memory | **Difficulty:** Medium

**Q: What is Demand Paging?**

**A:**
- Demand paging loads a page into memory only when it is actually referenced, not in advance.
- It reduces memory usage and speeds up process startup time.
- If a required page isn't in memory, it triggers a **page fault**, and the OS fetches it from disk.
- It's the standard technique used to implement virtual memory.

---

### Question 49
**Topic:** Virtual Memory | **Difficulty:** Medium

**Q: What is a Page Fault?**

**A:**
- A page fault is a trap raised when a process tries to access a page not currently in physical memory.
- The OS handles it by locating the page on disk, loading it into a free frame, and updating the page table.
- The process then resumes from where it left off.
- Frequent page faults degrade performance significantly and can lead to thrashing.

---

### Question 50
**Topic:** Virtual Memory | **Difficulty:** Hard

**Q: What is Thrashing, and how do you prevent it?**

**A:**
- Thrashing occurs when the system spends more time swapping pages in/out than executing actual processes.
- It happens because too many processes are competing for too little memory.
- Symptoms: high CPU usage but very low actual throughput.
- Prevented by limiting the degree of multiprogramming, using the Working Set Model, or adding more RAM.

---

### Question 51
**Topic:** Virtual Memory | **Difficulty:** Hard

**Q: What is the Working Set Model?**

**A:**
- The working set is the set of pages a process actively references within a given time window (Δ).
- The OS allocates enough frames to hold a process's working set, reducing page faults.
- If a process's working set doesn't fit in its allocated memory, thrashing is likely.
- It helps the OS decide how many processes it can run simultaneously without overloading memory.

---
---

## Topic 10: Page Replacement Algorithms
**Difficulty: Hard**

### Question 52
**Topic:** Page Replacement Algorithms | **Difficulty:** Medium

**Q: What is the FIFO Page Replacement Algorithm?**

**A:**
- FIFO replaces the oldest page in memory when a new page needs to be loaded and memory is full.
- It's simple to implement using a queue.
- Drawback: it can suffer from **Belady's Anomaly**, where more frames cause more page faults.
- It doesn't consider how frequently or recently a page was actually used.

---

### Question 53
**Topic:** Page Replacement Algorithms | **Difficulty:** Medium

**Q: What is LRU Page Replacement? Why is it generally better than FIFO?**

**A:**
- LRU (Least Recently Used) replaces the page that hasn't been used for the longest time.
- It's better than FIFO because it uses actual usage history, aligning with locality of reference.
- It never suffers from Belady's Anomaly.
- Drawback: it needs extra hardware/software (counters or a stack) to track usage, making it costlier.

---

### Question 54
**Topic:** Page Replacement Algorithms | **Difficulty:** Medium

**Q: What is the Optimal Page Replacement Algorithm?**

**A:**
- Optimal replaces the page that won't be used for the longest time in the future.
- It gives the lowest possible page-fault rate of any algorithm.
- It's not practically implementable because it requires future knowledge of the reference string.
- It's used only as a theoretical benchmark to measure other algorithms against.

---

### Question 55
**Topic:** Page Replacement Algorithms | **Difficulty:** Hard

**Q: What is the Clock Algorithm?**

**A:**
- The Clock algorithm is an efficient approximation of LRU using a circular list with a reference bit per page.
- On a page fault, the "clock hand" checks each page's reference bit — if 0, replace it; if 1, reset it to 0 and move on.
- It gives near-LRU performance with much lower overhead.
- Also called the Second-Chance Algorithm; widely used in real operating systems.

---

### Question 56
**Topic:** Page Replacement Algorithms | **Difficulty:** Hard

**Q: What is Belady's Anomaly?**

**A:**
- It is the counter-intuitive situation where increasing the number of page frames increases the number of page faults, instead of decreasing them.
- It's observed in FIFO page replacement for certain reference strings.
- Stack-based algorithms like LRU and Optimal never exhibit this anomaly.
- It's a classic interview question used to test conceptual depth, not just memorized theory.

---

## Topic 11: File Systems
**Difficulty: Medium**

### Question 57
**Topic:** File Systems | **Difficulty:** Medium

**Q: What is a File System? What are the common File Allocation Methods?**

**A:**
- A file system organizes, stores, retrieves, and manages files/directories on secondary storage.
- **Contiguous Allocation** — file stored in consecutive blocks; fast access, but causes external fragmentation.
- **Linked Allocation** — blocks scattered, each pointing to the next; no external fragmentation, but slow random access.
- **Indexed Allocation** — a separate index block holds pointers to all file blocks; supports fast direct access (used in Unix/Linux inodes).

---

### Question 58
**Topic:** File Systems | **Difficulty:** Easy

**Q: What are the different Directory Structures?**

**A:**
- **Single-level** — all files in one directory; simple but causes naming conflicts.
- **Two-level** — each user gets a separate directory.
- **Tree-structured** — allows nested subdirectories, used in most modern OS.
- **Acyclic/General graph** — allows file sharing, but graph structures need cycle detection.

---

### Question 59
**Topic:** File Systems | **Difficulty:** Easy

**Q: What are the different File Access Methods?**

**A:**
- **Sequential access** — reads/writes data in order from beginning to end (like tape).
- **Direct/Random access** — jumps directly to any block using a block number (used in databases).
- **Indexed access** — uses an index to locate records quickly, combining benefits of both.
- Choice depends on application needs — sequential for logs, direct for databases.

---

### Question 60
**Topic:** File Systems | **Difficulty:** Medium

**Q: How does File Protection work in an OS?**

**A:**
- File protection restricts unauthorized access using access control lists or permission bits (read/write/execute for owner/group/others).
- Passwords, encryption, and access control lists also protect files.
- The OS checks permissions before allowing any file operation.
- It ensures data confidentiality, integrity, and prevents accidental or malicious modification.

---
---

## Topic 12: Disk Scheduling
**Difficulty: Hard**

### Question 61
**Topic:** Disk Scheduling | **Difficulty:** Easy

**Q: Why is Disk Scheduling needed?**

**A:**
- Disk I/O is much slower than CPU/memory operations, so the order of servicing requests greatly affects performance.
- Disk scheduling minimizes seek time — the time for the read/write head to reach the right track.
- Good scheduling improves throughput and reduces average response time.
- It's essential in multi-user/multi-process systems with many concurrent disk requests.

---

### Question 62
**Topic:** Disk Scheduling | **Difficulty:** Medium

**Q: Explain FCFS and SSTF Disk Scheduling.**

**A:**
- FCFS services disk requests in the order they arrive — simple and fair, but can cause long seek times if requests are scattered.
- SSTF (Shortest Seek Time First) services the request closest to the current head position, reducing average seek time.
- Drawback of SSTF: it can cause starvation for requests far from the current head if closer ones keep arriving.
- FCFS never starves any request, but is generally less efficient.

---

### Question 63
**Topic:** Disk Scheduling | **Difficulty:** Medium

**Q: What is the difference between SCAN and CSCAN?**

**A:**
- SCAN (elevator algorithm) moves the head in one direction servicing requests, reaches the end, then reverses.
- CSCAN also moves in one direction, but jumps back to the beginning without servicing on the return trip.
- SCAN gives faster average response but less uniform wait times.
- CSCAN sacrifices some speed for more uniform, fair wait times across all requests.

---

### Question 64
**Topic:** Disk Scheduling | **Difficulty:** Hard

**Q: What is the difference between LOOK and CLOOK?**

**A:**
- LOOK is similar to SCAN, but the head only goes as far as the last pending request, not the disk's physical end.
- CLOOK is similar to CSCAN, but jumps back to the first pending request instead of the disk's beginning.
- Both LOOK and CLOOK avoid unnecessary head movement compared to SCAN/CSCAN.
- This makes them more efficient in practice, since real disks rarely have requests at the extreme ends.

---

### Question 65
**Topic:** Disk Scheduling | **Difficulty:** Medium

**Q: What are common Disk Performance Metrics?**

**A:**
- **Seek Time** — time to move the disk arm to the correct track.
- **Rotational Latency** — time for the desired sector to rotate under the head.
- **Transfer Time** — time to actually transfer the data.
- **Total Access Time = Seek Time + Rotational Latency + Transfer Time.**

---

## Topic 13: System Calls & Interrupts
**Difficulty: Medium**

### Question 66
**Topic:** System Calls & Interrupts | **Difficulty:** Easy

**Q: What is a System Call? What are its types?**

**A:**
- A system call is how a user application requests a service from the OS kernel (like file access or process creation).
- It switches the CPU from user mode to kernel mode temporarily.
- Types: Process control (fork, exec), File management (open, read, write), Device management (ioctl), Information maintenance (getpid), and Communication (pipe, socket).
- After the kernel completes the service, control returns to the user process.

---

### Question 67
**Topic:** System Calls & Interrupts | **Difficulty:** Medium

**Q: What is the difference between Interrupt, Trap, and Exception?**

**A:**
- An **Interrupt** is a signal from hardware (keyboard, timer, disk) that asynchronously alerts the CPU.
- A **Trap** (software interrupt) is intentionally triggered by a program, typically to invoke a system call.
- An **Exception** is an unexpected event during execution, like division by zero or invalid memory access.
- All three cause the CPU to pause current execution and run a specific handler routine.

---

### Question 68
**Topic:** System Calls & Interrupts | **Difficulty:** Medium

**Q: What is the difference between Polling and Interrupts?**

**A:**
- Polling is when the CPU repeatedly checks a device's status in a loop to see if it needs attention.
- This wastes CPU cycles if the device is rarely ready.
- Interrupts let the device signal the CPU only when it actually needs attention, freeing the CPU otherwise.
- Interrupts are more efficient for most real-world scenarios; polling suits very frequent, predictable events.

---

### Question 69
**Topic:** System Calls & Interrupts | **Difficulty:** Medium

**Q: What is DMA (Direct Memory Access)?**

**A:**
- DMA allows peripheral devices (like disk, network card) to transfer data directly to/from memory without CPU involvement for every byte.
- The CPU just initiates the transfer and is freed to do other tasks.
- The DMA controller handles the actual transfer and interrupts the CPU only when done.
- It significantly reduces CPU overhead for large data transfers like disk I/O and video streaming.

---
---

## Topic 14: I/O Management
**Difficulty: Medium**

### Question 70
**Topic:** I/O Management | **Difficulty:** Medium

**Q: What is the difference between Buffering, Caching, and Spooling?**

**A:**
- **Buffering** temporarily stores data during transfer between two devices of different speeds, smoothing out mismatches.
- **Caching** stores a copy of frequently accessed data in faster memory to speed up future access.
- **Spooling** queues jobs (like print jobs) on disk so a slow device can process them independently while other work continues.
- All three improve overall system efficiency but solve different problems.

---

### Question 71
**Topic:** I/O Management | **Difficulty:** Easy

**Q: What are Device Drivers?**

**A:**
- A device driver is software that lets the OS communicate with a specific hardware device.
- It translates generic OS calls into device-specific commands.
- Each hardware device (printer, GPU, keyboard) needs its own driver.
- Drivers run mostly in kernel mode for direct hardware access.

---

### Question 72
**Topic:** I/O Management | **Difficulty:** Medium

**Q: What is I/O Scheduling?**

**A:**
- I/O scheduling determines the order in which pending I/O requests are serviced, similar to CPU/disk scheduling.
- It aims to maximize throughput, ensure fairness, and minimize wait time for I/O-bound processes.
- The OS maintains a queue per device and applies a scheduling policy.
- It works closely with disk scheduling algorithms like SCAN and C-SCAN.

---

### Question 73
**Topic:** I/O Management | **Difficulty:** Medium

**Q: Why is I/O considered the slowest part of a computer system, and how does the OS deal with it?**

**A:**
- I/O devices operate at mechanical/electronic speeds far slower than CPU/RAM speeds, creating a major bottleneck.
- The OS uses buffering, caching, spooling, DMA, and interrupts to reduce the CPU's exposure to slow I/O.
- Asynchronous I/O lets a process continue other work while I/O completes in the background.
- Efficient I/O management is critical to overall system throughput.

---
---

## Topic 15: Protection & Security
**Difficulty: Hard**

### Question 74
**Topic:** Protection & Security | **Difficulty:** Easy

**Q: What is the difference between Authentication and Authorization?**

**A:**
- Authentication verifies **who** a user is (password, biometrics, OTP).
- Authorization determines **what** an authenticated user is allowed to do (permissions, access rights).
- Authentication always happens first; authorization happens after.
- Example: logging in is authentication; being allowed to edit a specific file is authorization.

---

### Question 75
**Topic:** Protection & Security | **Difficulty:** Medium

**Q: What is Access Control and a Protection Domain?**

**A:**
- Access control restricts which users/processes can access specific resources, using ACLs or permission bits.
- A Protection Domain defines the set of resources a process can access and what operations it can perform.
- Each process operates within a domain, and domains can change during execution.
- This limits the damage a compromised process can cause to the rest of the system.

---

### Question 76
**Topic:** Protection & Security | **Difficulty:** Hard

**Q: What is an Access Matrix?**

**A:**
- An Access Matrix is a conceptual model of the protection state, with rows as domains and columns as objects.
- Each cell lists the operations a domain is allowed to perform on that object.
- It's a theoretical tool; in practice it's implemented as Access Control Lists (per-object) or Capability Lists (per-domain).
- It helps design and reason about real-world protection systems.

---

### Question 77
**Topic:** Protection & Security | **Difficulty:** Medium

**Q: What are common OS Security Threats?**

**A:**
- **Malware** (viruses, worms, trojans) that exploit vulnerabilities to damage or steal data.
- **Buffer overflow** attacks that overwrite memory to execute malicious code.
- **Denial-of-Service (DoS)** attacks that overload system resources.
- **Privilege escalation**, where an attacker gains higher access rights than intended; defended using patches, firewalls, and sandboxing.

---

## Topic 16: Multiprocessing & Parallelism
**Difficulty: Medium**

### Question 78
**Topic:** Multiprocessing & Parallelism | **Difficulty:** Medium

**Q: What is the difference between Multiprogramming, Multitasking, and Multiprocessing?**

**A:**
- **Multiprogramming** keeps multiple programs in memory so the CPU always has something to execute — single CPU, no real simultaneity.
- **Multitasking** allows a single CPU to switch rapidly between multiple tasks, giving the illusion of simultaneous execution.
- **Multiprocessing** uses multiple CPUs/cores to genuinely execute multiple processes in parallel.
- Multiprocessing gives true parallelism; multitasking only gives the appearance of it on one CPU.

---

### Question 79
**Topic:** Multiprocessing & Parallelism | **Difficulty:** Easy

**Q: What is a Time-Sharing System?**

**A:**
- A time-sharing system allows multiple users to interact with a computer simultaneously by rapidly switching the CPU between them.
- Each user gets a fair time slice, giving quick response times.
- It makes the system feel interactive and dedicated to each individual user.
- It's the basis of modern multitasking operating systems.

---

### Question 80
**Topic:** Multiprocessing & Parallelism | **Difficulty:** Medium

**Q: What is Parallel Processing?**

**A:**
- Parallel processing is executing multiple instructions or processes simultaneously using multiple processors/cores.
- It's used for computation-heavy tasks like scientific simulations, video rendering, and machine learning.
- It requires careful synchronization to avoid race conditions between parallel tasks.
- It's different from multitasking, which only simulates simultaneity on a single core.

---

### Question 81
**Topic:** Multiprocessing & Parallelism | **Difficulty:** Medium

**Q: What is a Real-Time Operating System (RTOS), and how is it different from a general-purpose OS?**

**A:**
- RTOS guarantees a task will complete within a strict, predictable time limit — used in embedded, medical, and aerospace systems.
- Hard real-time systems must never miss deadlines (e.g., pacemaker); soft real-time can occasionally miss deadlines (e.g., video streaming).
- A general-purpose OS optimizes for average throughput and fairness; RTOS optimizes for predictability.
- Examples of RTOS: VxWorks, FreeRTOS.

---
---

## Topic 17: Linux & Windows Basics
**Difficulty: Medium**

### Question 82
**Topic:** Linux & Windows Basics | **Difficulty:** Easy

**Q: Briefly explain Linux Architecture.**

**A:**
- Layers: Hardware → Kernel (monolithic, manages processes/memory/devices) → Shell → Applications/Utilities.
- The kernel provides system calls that applications use to interact with hardware.
- It's open-source and highly customizable, widely used in servers.
- Common distributions: Ubuntu, CentOS, Red Hat.

---

### Question 83
**Topic:** Linux & Windows Basics | **Difficulty:** Medium

**Q: What is the difference between Linux and Windows?**

**A:**
- Linux is open-source and free; Windows is proprietary and licensed.
- Linux is dominant in servers, Windows is dominant in desktop/enterprise environments.
- Linux is CLI-first with a case-sensitive file system; Windows is primarily GUI-driven.
- Linux offers stronger built-in permission control; Windows has broader commercial software and driver support.

---

### Question 84
**Topic:** Linux & Windows Basics | **Difficulty:** Easy

**Q: Name some commonly used Linux Commands and their purpose.**

**A:**
- `ls`, `cd`, `pwd` — list directory contents, change directory, show current path.
- `chmod`, `chown` — change file permissions and ownership.
- `ps`, `top` — show running processes and resource usage.
- `grep`, `find`, `kill` — search text, find files, and terminate processes.

---

### Question 85
**Topic:** Linux & Windows Basics | **Difficulty:** Medium

**Q: What is Shell Scripting, and why is it useful?**

**A:**
- A shell script is a text file containing a sequence of Linux commands, executed together (usually a `.sh` file run via bash).
- It's used to automate repetitive tasks like backups, deployments, and log monitoring.
- It supports variables, loops, and conditionals like a programming language.
- Widely used by DevOps engineers and system administrators for automation.

---
---

## Topic 18: Miscellaneous Important Concepts
**Difficulty: Medium**

### Question 86
**Topic:** Miscellaneous Important Concepts | **Difficulty:** Medium

**Q: What is the difference between Cache and Buffer?**

**A:**
- Cache stores a copy of frequently/recently accessed data in faster memory, meant to be reused repeatedly.
- Buffer temporarily holds data during a transfer between two devices of different speeds, and is typically used once.
- Cache improves performance through repeated reuse; buffer improves performance by smoothing speed mismatches.
- Example: CPU cache vs. a print buffer.

---

### Question 87
**Topic:** Miscellaneous Important Concepts | **Difficulty:** Medium

**Q: What is Virtualization, and what is a Hypervisor?**

**A:**
- Virtualization creates a virtual, software-based version of hardware resources, allowing multiple OS to run on one physical machine.
- A Hypervisor is the software layer that creates and manages virtual machines, allocating physical resources among them.
- Type 1 (bare-metal) hypervisors run directly on hardware (e.g., VMware ESXi); Type 2 run on a host OS (e.g., VirtualBox).
- It enables better hardware utilization and isolation between environments.

---

### Question 88
**Topic:** Miscellaneous Important Concepts | **Difficulty:** Medium

**Q: What is the difference between Containers and Virtual Machines?**

**A:**
- VMs virtualize entire hardware, each running its own full OS, managed by a hypervisor — heavier, but strongly isolated.
- Containers virtualize at the OS level, sharing the host kernel while isolating applications — lightweight and fast to start.
- Docker is a popular containerization platform.
- Containers suit microservices; VMs suit running different OS or needing stronger isolation.

---

### Question 89
**Topic:** Miscellaneous Important Concepts | **Difficulty:** Easy

**Q: What are Throughput, Turnaround Time, Waiting Time, and Response Time?**

**A:**
- **Throughput** — number of processes completed per unit time.
- **Turnaround Time** — total time from submission to completion.
- **Waiting Time** — total time a process spends in the ready queue.
- **Response Time** — time from submission until the first response is produced.

---

### Question 90
**Topic:** Miscellaneous Important Concepts | **Difficulty:** Medium

**Q: What is the difference between Virtual Memory and Physical Memory in terms of performance?**

**A:**
- Physical memory (RAM) is fast, limited in size, and directly accessed by the CPU.
- Virtual memory extends this using disk space, allowing larger address spaces at the cost of slower access when swapping is involved.
- Over-reliance on virtual memory (excessive paging) degrades performance — this is thrashing.
- A well-tuned system keeps active data in RAM and uses virtual memory only as overflow.

---

## Topic 19: Scenario-Based Questions
**Difficulty: Hard**

### Question 91
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Why is Round Robin preferred in time-sharing systems?**

**A:**
- Round Robin gives every process a fixed time quantum in rotation, ensuring no process waits indefinitely.
- This fairness matters in time-sharing systems, where multiple interactive users expect quick responses.
- It optimizes for good average response time, which matters more than turnaround time for interactive use.
- The trade-off is choosing an optimal time quantum to balance responsiveness against context-switch overhead.

---

### Question 92
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Which scheduling algorithm would you use in a hospital emergency system, and why?**

**A:**
- A preemptive Priority Scheduling approach, layered with real-time OS principles, so critical alerts are always handled first.
- Preemptive priority scheduling lets a higher-priority emergency task interrupt a lower-priority one immediately.
- Aging can be added so lower-priority but still important tasks aren't starved indefinitely.
- Plain FCFS or Round Robin would be unsuitable, since they treat all requests equally — unacceptable in life-critical scenarios.

---

### Question 93
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Why is Paging generally preferred over Segmentation in modern OS?**

**A:**
- Paging uses fixed-size blocks, which completely eliminates external fragmentation, unlike segmentation.
- It's simpler for the OS to manage since all pages/frames are the same size.
- It also makes memory allocation and address translation more efficient through page tables.
- Segmentation is still useful for reflecting logical program structure, so systems like x86 combine both.

---

### Question 94
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Explain a Deadlock using a real-life traffic example.**

**A:**
- Picture four cars at a four-way intersection, each waiting to move into a section blocked by the car ahead — a cycle where no car moves first.
- This mirrors **circular wait**, one of the four necessary conditions for deadlock.
- Just as a traffic controller resolves this by asking one car to back up (preemption), an OS breaks deadlock by forcibly releasing a resource.
- It illustrates why breaking any one of the four necessary conditions prevents deadlock.

---

### Question 95
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Why is LRU generally better than FIFO for page replacement?**

**A:**
- LRU uses actual page usage history, aligning with the principle of locality — recently used pages are likely to be used again.
- FIFO ignores usage patterns and can evict a frequently used page just because it was loaded first.
- LRU never suffers from Belady's Anomaly, while FIFO can.
- The trade-off is that LRU needs more overhead to track access history accurately.

---

### Question 96
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: What happens internally when you double-click an application icon?**

**A:**
- The OS locates the executable file and creates a new process, allocating a PCB and initial memory segments.
- It loads required pages into memory (often via demand paging) and sets up the program counter.
- The process moves into the Ready queue, and the CPU scheduler eventually assigns it CPU time.
- The OS also initializes the application's window and links any needed shared libraries (DLLs/.so files).

---

### Question 97
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: How does Context Switching affect system performance?**

**A:**
- Every context switch is pure overhead — saving/restoring registers, updating memory maps, and often invalidating CPU cache.
- Frequent context switching (e.g., very small Round Robin quantum) increases this overhead and reduces effective throughput.
- Too little context switching (e.g., large quantum, FCFS) hurts responsiveness for interactive systems.
- OS designers balance switching frequency against overhead based on the workload type.

---

### Question 98
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Why do Operating Systems use Virtual Memory?**

**A:**
- It allows programs larger than physical RAM to run, keeping only actively used pages in memory.
- It provides process isolation, since each process gets its own private virtual address space.
- It enables efficient multiprogramming, letting more processes run than would fit in physical RAM alone.
- The trade-off is potential performance loss if page faults become too frequent — thrashing.

---

### Question 99
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Explain Process Synchronization using a printer-sharing example.**

**A:**
- If multiple processes send print jobs to one shared printer simultaneously, their outputs could interleave into garbled printouts — a critical section problem.
- A semaphore or mutex lock ensures only one process accesses the printer at a time, while others wait.
- Once the current job finishes, the lock is released and the next process gets access.
- Spooling is also commonly used here — jobs are queued on disk and printed one at a time in order.

---

### Question 100
**Topic:** Scenario-Based | **Difficulty:** Hard

**Q: Why are Semaphores required in multithreaded applications?**

**A:**
- Multiple threads sharing memory can create race conditions if they access shared data without coordination.
- Semaphores act as signaling counters, letting threads coordinate access to limited shared resources.
- They block threads when a resource is unavailable and wake them when it's free.
- Without proper synchronization, multithreaded applications produce unpredictable, hard-to-debug bugs.

---
---

# ⭐ Top 30 Most Frequently Asked Operating System Questions in TCS

*Your final rapid-fire revision list — these come up again and again across TCS Prime, TCS Digital, and TCS Ninja interviews. Full explanations are in the sections above; here's the one-line "say-this" answer.*

1. **What is an OS?** — System software that interfaces between user and hardware, managing resources like CPU, memory, and I/O.
2. **Types of OS** — Batch, Time-Sharing, Distributed, Real-Time.
3. **Process vs Thread** — Process has its own memory; threads share memory within a process and are lighter to create.
4. **Process States** — New → Ready → Running → Waiting → Terminated.
5. **What is a PCB?** — Data structure storing process ID, state, registers, and memory info — used during context switching.
6. **What is Context Switching?** — Saving current process state and loading the next process's state; pure overhead, no useful work.
7. **Advantages of Multithreading** — Better CPU utilization, responsiveness, and efficient resource sharing.
8. **CPU Scheduling Algorithms** — FCFS, SJF, SRTF, Priority, Round Robin, MLQ, MLFQ.
9. **Preemptive vs Non-preemptive** — Preemptive can interrupt a running process; non-preemptive runs to completion or yield.
10. **Round Robin** — Fixed time quantum per process in rotation; ideal for time-sharing systems.
11. **Starvation & Aging** — Starvation is indefinite waiting due to low priority; Aging gradually raises priority to fix it.
12. **Critical Section** — Code segment accessing shared resources; needs mutual exclusion, progress, bounded waiting.
13. **Mutex vs Semaphore** — Mutex is a lock with ownership; semaphore is a signaling counter, usable across processes.
14. **Producer-Consumer Problem** — Classic synchronization problem solved using `full`, `empty`, and `mutex` semaphores.
15. **Dining Philosophers Problem** — Classic deadlock/synchronization problem illustrating circular resource contention.
16. **What is a Deadlock?** — A set of processes blocked forever, each waiting on a resource held by another in the cycle.
17. **4 Necessary Conditions for Deadlock** — Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait.
18. **Prevention vs Avoidance** — Prevention removes a necessary condition entirely; Avoidance checks for a "safe state" before allocating (e.g., Banker's Algorithm).
19. **Banker's Algorithm** — Grants resource requests only if the system remains in a safe state.
20. **Paging vs Segmentation** — Paging uses fixed-size blocks (no external fragmentation); segmentation uses variable-size logical units (can fragment).
21. **Internal vs External Fragmentation** — Internal wastes space inside a block; external wastes space between scattered free blocks.
22. **What is Virtual Memory?** — Illusion of large continuous memory using disk as an extension of RAM.
23. **What is a Page Fault?** — Trap raised when a needed page isn't in memory; OS loads it from disk.
24. **What is Thrashing?** — System spends more time swapping pages than executing processes, due to memory overcommitment.
25. **LRU vs FIFO** — LRU uses actual access history and avoids Belady's Anomaly; FIFO just evicts the oldest page.
26. **Belady's Anomaly** — More page frames unexpectedly causing more page faults (seen in FIFO).
27. **Monolithic vs Microkernel** — Monolithic runs all services in kernel space (fast, less stable); Microkernel keeps kernel minimal (stable, more modular).
28. **What is a System Call?** — A request from a user program to the kernel for a service, switching to kernel mode.
29. **Multiprogramming vs Multitasking vs Multiprocessing** — Multiple programs in memory vs. rapid task switching on one CPU vs. true parallel execution on multiple CPUs.
30. **Linux vs Windows** — Linux is open-source, CLI-first, server-dominant; Windows is proprietary, GUI-first, desktop/enterprise-dominant.

---

## Final Tip Before Your TCS Prime Interview

Say your answers the way they're written here — **short, structured, and confident**. If the interviewer asks a follow-up, expand using the detailed answer from the matching topic section above. Good luck! 🎯
