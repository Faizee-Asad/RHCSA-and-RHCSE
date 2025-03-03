# Process 

* When we install a program, it gets stored on hard drive.
* This installed program on hard drive is of no direct use to us.
* To use a program, we must run it.
* System runs a program on RAM.
* This running instance of a program is called a **process**.
* When a process of a program starts, the system creates a special environmnet for that program.
* That environment contains everything needed for the system to run the program as if no other program were running on the system.

* When we issue a command, bash finds the program's binary on hard drive and loads it on RAM.
* On RAM, the process of the program starts.
* Linux is a multi-user system which mean different users can run various programs, each running instance of a program must be identified uniquely by the kernel.
* Hence, system assigns a maximum 5-digit ID to every process called PID (Process ID).
* PIDs can range from 1 to 99999
* PID of each process on the system is unique and is incremental by 1.
* Once all PIDs are used up, system will repeat the PID number which are released by privous processes.
* At any point of time, no two processes with the same PID exist in the system because it is the PID that Linux uses to track each process.
* If 2 users paralleling start vi editor, the name of both processes will be same but their PIDs will be unique.
* Processes run in parent child heirarchy.
* **Parent processes:** These are processes that create other processes during run-time.
* **Child processes:** These are processes ar created by other processes during run-time.
* Every process has two ID numbers assigned to it: The process ID (PID) and the Parent process ID (PPID)
* Most of the commands that you run have the shell (bash) as their parent

* Operating System has 2 parts: **user space and kernel space**
* When the Operating system starts, both its user space and kernel space are loaded.
* **systemd** process loads the entire user space.
* **kthreadd** process loads the entire kernel space.
* systemd is the first process that runs on system start up and kthreadd is the second.
* Hence, PID 1 is always given to systemd and PID 2 to kthreadd
* systemd and kthreadd are started by the kernel itself
* Hence, their PPID is always 0.

* There are fundamentally two type of processes in Linux:
1. Foreground processes: By default, every process that you start runs in the foreground. it gets it's input from the keyboard and sends its output to the screen.
2. Background processes: These processes are not connected to a terminal; they don't expect any user input.

*  There are various states of a process.
1. Running (R): in this state, the process is actively executing task using the CPU cycles.
2. Waiting/Sleep (I/S): in this state, a process is sleeping  (not using CPU cycles) and waiting for an event to occur so that it can change to running state and perform execution.
```
Sleep processe are futher divided into 2 types:
1. Interruptible - can be interrupted or called by another process.
2. Uninterruptible - cannot be interrupted from sleep state
```
3. Stopped (T): in this state, a process is still on RAM but has been stopped or suspended. Such processes cannot run automactically. We need to start or resume them manually.
4. Zombie (D): this is a dead or corrupted process

* The fundamental way of controlling processes in Linux is by sending signals to them.
* There are multiple signals that you can send to a process, to view all the signals run command **kill -l**.
* And most signals are for internal use by the system, or for programmers when they write code.
* The following are signals which are useful to a sysem user:
```
* HUP (1)     -      used to kill a foreground process when its terminal is closed.
* INT (2)     -      used to kill a process when used does ctrl + c
* KILL (9)    -      used to abruptly kill a process
* TERM (15)   -      used to kill a process gracefully.
* CONT (18)   -      used to resume / start a suspended / stopped process
* STOP (19)   -      used to stop / suspend a process 
```
* **kill, killall or pkill** commands are used to send signals and manage processes.
* Kill only understand PID of a process where as killall only understand the process by name.
* pkill is mostly used to manage processes of a particular user

```
top command is used in all Linux flavors to perform live monitoring of top running processes
```

```
# pidof crond (pidof command is used to find out the process IDs of a specific running program)
# pidof crond atd bash

# echo $$ ($$ is the PID of the current process.)

# sleep 10 (sleep command is used to create a dummy job.)
# jobs (jobs command in Linux lists jobs that are running, stopped, or otherwise in the current shell environment)

# sleep 10000 & (Run this command in background. & is used to run command in the background. by default command run in foreground.)
# sleep 20000 &
# jobs (check list of background process)

# fg %2 (The fg command brings a background process to the foreground) (Ctrl + Z to stop the proocess)
# jobs
# bg %2 (The bg command moves a stopped process from the foreground to the background ) 
# jobs
```
```
# ps displays information about a selection of the active processes
# ps aux|less
# ps lax|less
# ps -el|less
# ps -eo comm,pid,ppid

# top (top command is used to show the Linux processes)
```
```
# ps -el | awk '/D/ {print $2}'
# ps -el | grep "D"

# ps -el | grep atd
# kill -19 1647 (STOP (19) - used to stop / suspend a process)
# ps -el | grep atd
# killall -18 atd (CONT (18) - used to resume / start a suspended / stopped process)

# ps -el | grep atd

# su abc
# bc

# pkill bc -u abc
# pkill -9 bc -u abc (KILL (9) - used to abruptly kill a process)
# pkill -2 bc -u abc (INT (2) - used to kill a process when used does ctrl + c)
```
