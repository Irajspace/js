# Operating System

## What does an Operating System do?

- Memory Management  
- I/O Management  
- CPU Scheduling  
- Multitasking / Multiprogramming  

## The only thing running at all times is kernel

![alt text](os-images/image.png)

## What makes something a system

- There is a connection with each interrelated parts means there is complexity of o(n2)
To overcome this one has to come up with apis to level down this complexity

## Hardware and software

- There are registers on processors which pointing to parts of memory that allows the program to run. In between there may be caches that make system fast 
Then there is page table and TLB that make virtual memory 
The OS abstracts these abstracts the hardware details from the application
![alt text](os-images/image-1.png)


## Abstraction
 
- We are creating a abstraction of hardware
 like for processor-threads, memory-address spaces,storage-files, networks-sockets

 that process can run all these abstracted details

 - Above this there is another layer of abstraction called system libs ,security libs which allow you to do ssl on
 ![alt text](os-images/image-2.png)

 Each processes are running at a time and each give isolation to each other
 ![alt text](os-images/image-3.png)
 here you can see system libraries are linked into our program which is later converted into bits by compiler and then run by processes
 
 # Process
 ![alt text](os-images/image-4.png)
 ![alt text](os-images/image-5.png)

 # The illusion of multiple processors

 - Here what we do is we try to switch alternate between the two processes so fast we thought we are having two processors. the registers are pointing towards green or brown memory where it is left off
 ![alt text](os-images/image-6.png)
 ![alt text](os-images/image-7.png)

 # Abstraction
 ![alt text](os-images/image-8.png)
 ![alt text](os-images/image-9.png)
 ![alt text](os-images/image-10.png)

# Instruction cycle
- So what happens is program counter present at processor points to memory allow the processor to have set of instructions . It pulls the instructions in from the memory and decode it and then we execute it

Now under this 

## Thread
  It got its own program counter, registers,execution flags, memory stack
  ![alt text](os-images/image-11.png)
  ![alt text](os-images/image-12.png)
  ![alt text](os-images/image-13.png)
  A CPU has registers, including the Program Counter (PC), which points to the next instruction in memory. The CPU fetches that instruction, decodes it, and executes it. The thread’s execution state (context) is partly stored in registers and partly in memory.(TCB-> thread control block)
  ![alt text](os-images/image-14.png)
  ![alt text](os-images/image-15.png)
  ![alt text](os-images/image-16.png)

## Address Space
   ![alt text](os-images/image-17.png)
   whats in heap segment ->things allocated with malloc
   ![alt text](os-images/image-18.png)

## Protection
   How OS can protect
   ![alt text](os-images/image-19.png)
   ![alt text](os-images/image-20.png)
   - With base and bound it is like hardware type check means the address space should be greater than base and it should be less than bound

   Adress space translation
   ![alt text](os-images/image-21.png)
   ![alt text](os-images/image-22.png)
    - Page tables is used to convert virtual address into physical ones

## PRocess
 ![alt text](os-images/image-23.png)
 Tradeoff-
 ![alt text](os-images/image-24.png)

## Multithreading or single-threading
 ![alt text](os-images/image-25.png)
 ![alt text](os-images/image-26.png)

![alt text](os-images/image-27.png)
process is a container and thread is an execution element

## Why do we need processes
 ![alt text](os-images/image-28.png)

## Fourth OS concept
  ![alt text](os-images/image-29.png)
  ![alt text](os-images/image-31.png)
  ![alt text](os-images/image-32.png)
  in system mode base and bound is ignored because we have full spaces

  These are the ways we can go from user mode to kernel mode
  ![alt text](os-images/image-33.png)
  - This interrupt table is already loaded in os boots and run the execution that whether to switch from process a to process b
  ![alt text](os-images/image-34.png)
![alt text](os-images/image-35.png)
![alt text](os-images/image-36.png)

## MEMORY management
![alt text](os-images/image-37.png)
![alt text](os-images/image-38.png)

## Adding Thread
![alt text](os-images/image-39.png)
![alt text](os-images/image-40.png)
Here one can interlave between threads mean one can go and leave and do other job

## Facts
![alt text](os-images/image-41.png)

## Switching
Here in 2nd case there is blockage due to I/O operation that is the reason it cant interleave between threads
![alt text](os-images/image-42.png)
![alt text](os-images/image-43.png)
- In multithreaded processes, one can share data betweensame adresses ... means same processes

![alt text](os-images/image-44.png)

Clearance
![alt text](os-images/image-45.png)
![alt text](os-images/image-46.png)

posix threads
![alt text](os-images/image-47.png)

# The way we can read this is go from inside to out star routine is a pointer to a function that takes a void * and return a void *
 - Thread join means until thread is not completed it will not go 
![alt text](os-images/image-49.png)
special trap instruction lets you jump from user mode to kernel mode and find out it is not error it is used to create thread and this is wrapper around system call
![alt text](os-images/image-50.png)
You see this means until and unless all thread is not completed till finally then only parent thread will continue

![alt text](os-images/image-51.png)

- The first argument is no of arguments passed 
Lets take an example ./program.out 5 
here no of arguments passed is 2 
arg[0]="./program.out
arg[1]="5"

So basically what is happening is we are taking no of threads we want to create if we dont pass we are taking default as 2 
Then what are we doing is we are creating threads and joining as a parent thread

![alt text](os-images/image-52.png)
It is going to look like this
Here you can see the thread is not having same exact order
means it is not sequential because it got interleaved
![alt text](os-images/image-53.png)
Here pink stack grows long it can cause error in bluse stack
![alt text](os-images/image-54.png)

# INTERLEAVING AND INDETERMINSM
illusion is all threads run in a processes run but actually some of the run and some dont
![alt text](os-images/image-56.png)
![alt text](os-images/image-55.png)
![alt text](os-images/image-57.png)
![alt text](os-images/image-58.png)
Here you can see racing conditions happens
Although in Js 
we are it is single threaded it causes racing condition because of async code

![alt text](os-images/image-60.png)
![alt text](os-images/image-59.png)

## Threads cant share stack 
- beacuse is stack we have state stored
![alt text](os-images/image-61.png)
SOlution
![alt text](os-images/image-62.png)

# LOCKS
![alt text](os-images/image-63.png)
![alt text](os-images/image-64.png)

# How are we gonna lock it
![alt text](os-images/image-65.png)
![alt text](os-images/image-66.png)

# How are the processes start
![alt text](os-images/image-67.png)

![alt text](os-images/image-68.png)it
![alt text](os-images/image-69.png)
fork creates a process
it copies a process into another adr  ess space 
![alt text](os-images/image-70.png)
![alt text](os-images/image-71.png)
![alt text](os-images/image-72.png)
![alt text](os-images/image-73.png)
![alt text](os-images/image-74.png)

# Fork race
![alt text](os-images/image-75.png)
this is how new program is created Here what happended throw all my adress spaces and creates a new program means execute new instrucitons
![alt text](os-images/image-77.png)
![alt text](os-images/image-76.png)
![alt text](os-images/image-78.png)

# SEMAPHORES
- Here you can see if there is some critical section means lock have to be applied before this code
- One can do Sempahore down means now value =1 and now if any other tries to get in means it will change semaphore value to zero 
so it will not let to do it
![alt text](os-images/image-79.png)
![alt text](os-images/image-81.png)
![alt text](os-images/image-82.png)
![alt text](os-images/image-83.png)

# SHARE HEAP BUT NOT STACK
![alt text](os-images/image-84.png)
![alt text](os-images/image-85.png)
sleep(1)-> pauses this thread for 1 second

# Starting a new program
![alt text](os-images/image-86.png)

# SIgnalling
![alt text](os-images/image-87.png)

So what happens is this will loop infinite until a signal comes if it comes it will take and exit
![alt text](os-images/image-88.png)
![alt text](os-images/image-89.png)

# FILES
![alt text](os-images/image-90.png)
![alt text](os-images/image-91.png)
![alt text](os-images/image-92.png)
![alt text](os-images/image-93.png)

WITH THE STDIN AND STDOUT ONE CAN REDIRECT TO ANYOTTHER FILE
![alt text](os-images/image-94.png)
![alt text](os-images/image-95.png)
Reason for int
![alt text](os-images/image-96.png)

Earlier we were taking char by char now we take in buffer
![alt text](os-images/image-97.png)
![alt text](os-images/image-98.png)

# Design patterns
![alt text](os-images/image-99.png)
![alt text](os-images/image-100.png)
![alt text](os-images/image-101.png)

4 th lecture again 

![alt text](os-images/image-102.png)
![alt text](os-images/image-103.png)
![alt text](os-images/image-104.png)

# What will be the output difference
![alt text](os-images/image-105.png)
YOu will see that after 10 seconds only everything will be outputed 
it stores in the buffer or until and unless new line is not there
![alt text](os-images/image-106.png)
![alt text](os-images/image-107.png)
![alt text](os-images/image-108.png)

![alt text](os-images/image-109.png)

# What can happen if buffer didnt get flushed
![alt text](os-images/image-110.png)
![alt text](os-images/image-111.png)
![alt text](os-images/image-112.png)
# this is the solution Write flush after buffering so that it writs on disk
![alt text](os-images/image-113.png)
![alt text](os-images/image-114.png)

![alt text](os-images/image-115.png)
# WHy do we need sys calls less
![alt text](os-images/image-116.png)
![alt text](os-images/image-117.png)
![alt text](os-images/image-119.png)
![alt text](os-images/image-118.png)
![alt text](os-images/image-120.png)
![alt text](os-images/image-121.png)

# Fork in a multi-threaded process
![alt text](os-images/image-122.png)
![alt text](os-images/image-123.png)
![alt text](os-images/image-124.png)
![alt text](os-images/image-125.png)

# IPC AND SOKCETS
![alt text](os-images/image-126.png)

# THe network Req cycle
![alt text](os-images/image-127.png)
🧠 The 12-Step Web Request Lifecycle
🔵 Phase 1: Receiving the Request from the Client
Step 1: read() syscall (network socket)
Server waits for incoming requests
Calls read() on socket → enters kernel mode
Step 2: Packet arrives (DMA + Interrupt)
Client sends HTTP request
Network card receives data
Uses DMA → directly writes into kernel buffer
Triggers interrupt → wakes up OS
Step 3: Kernel copy + RTU
Kernel copies data → user-space request buffer
Performs RTU (Return To User) → server resumes execution
🟡 Phase 2: Processing and Fetching the File
Step 4: Parse request
Server reads buffer
Parses request (e.g., GET /index.html)
Determines required file
Step 5: read() syscall (file read)
Server asks kernel to read file from disk
Step 6: Disk request
Kernel sends request to disk hardware
Disk locates required blocks
Step 7: Disk data (DMA + Interrupt)
Disk uses DMA → copies data to kernel buffer
Sends interrupt → notifies kernel
Step 8: Kernel copy + RTU
Kernel copies file data → user-space reply buffer
Returns control to server
🟢 Phase 3: Sending the Response
Step 9: Format reply
Server prepares HTTP response:
Headers (HTTP/1.1 200 OK)
File content
Step 10: write() syscall
Server asks kernel to send response via socket
Step 11: Kernel copy
Kernel copies data → network buffer
Step 12: Send via network (DMA)
Kernel instructs network card
Network card:
Formats packets
Sends to client using DMA
🔴 Hidden Lesson: Copy Overhead (VERY IMPORTANT)
Multiple data copies occur:
Step 3 → Kernel → User
Step 8 → Kernel → User
Step 11 → User → Kernel
Problems:
CPU overhead
Slow performance
Many context switches
🚀 Optimization Insight
Modern systems use zero-copy techniques
Example: sendfile()
Benefit:
Disk → Kernel → Network
(no user-space copy)
Skips:
Steps 8, 9, 10, 11
![alt text](os-images/image-128.png)

# Communication between process

- Process abstraction is designed to discourage inter-process communication
See here how process protects from each other
![alt text](os-images/image-129.png)
![alt text](os-images/image-130.png)

Why sharing data from data is expensive - beacuse everytime you have to read and write from disk
so forking for communication is expensive
- writing to file descriptor and reading from it

![alt text](os-images/image-131.png)

SOlution-
YOu can have shared data as as a space
![alt text](os-images/image-132.png)
![alt text](os-images/image-133.png)
   ![alt text](os-images/image-134.png)
   ![alt text](os-images/image-135.png)
   ![alt text](os-images/image-136.png)
   ![alt text](os-images/image-137.png)
   ![alt text](os-images/image-138.png)
   ![alt text](os-images/image-139.png)
   ![alt text](os-images/image-140.png)
   ![alt text](os-images/image-141.png)
   pipe is not a process its just a queue inside process
   ![alt text](os-images/image-142.png)
   Why does parent allow write and child allows read only explain
   ![alt text](os-images/image-143.png)
   ![alt text](os-images/image-144.png)
   ![alt text](os-images/image-145.png)
   ![alt text](os-images/image-146.png)

# EOF
![alt text](os-images/image-147.png)

# RPC
![alt text](os-images/image-148.png)

# How does sever knows about diff clients
- Ip address+port+protocol- makes communication channel unique
socket is a data structure including a queue
![alt text](os-images/image-149.png)

# Communication
![alt text](os-images/image-150.png)

# protocol of tcp/ip
- sequential order (data packets)
![alt text](os-images/image-151.png)
![alt text](os-images/image-152.png)
![alt text](os-images/image-153.png)
![alt text](os-images/image-154.png)
![alt text](os-images/image-155.png)
![alt text](os-images/image-156.png)
Socket protocol
![alt text](os-images/image-157.png)
Here child only listens to read and write and dont take new client whereas parent socket is responseible for listening new client
![alt text](os-images/image-158.png)

# Concurrent sockets
if you remove wait from parent this will become concurrent
![alt text](os-images/image-159.png)

# creating address
![alt text](os-images/image-160.png)
![alt text](os-images/image-161.png)
# sockets without protection
![alt text](os-images/image-162.png)
![alt text](os-images/image-163.png)
![alt text](os-images/image-164.png)
![alt text](os-images/image-165.png)
![alt text](os-images/image-166.png)
![alt text](os-images/image-167.png)

# Synchronisation
![alt text](os-images/image-168.png)

# Context switch in a single threaded process
![alt text](os-images/image-169.png)
![alt text](os-images/image-170.png)
![alt text](os-images/image-171.png)
![alt text](os-images/image-172.png)
![alt text](os-images/image-173.png)

# Shared vs Per thread state
internal events gets voluntarily returned

![alt text](os-images/image-174.png)
![alt text](os-images/image-175.png)
![alt text](os-images/image-176.png)
# Switching
first it unloads then it loads
![alt text](os-images/image-177.png)
![alt text](os-images/image-178.png)

# Context switching
there are two types
- THRead switching
- Process switching
![alt text](os-images/image-179.png)
![alt text](os-images/image-180.png)
![alt text](os-images/image-181.png)
![alt text](os-images/image-182.png)
![alt text](os-images/image-183.png)
![alt text](os-images/image-184.png)

# Facts
![alt text](os-images/image-185.png)
![alt text](os-images/image-186.png)

# Interrupt
![alt text](os-images/image-187.png)
![alt text](os-images/image-188.png)
![alt text](os-images/image-189.png)
![alt text](os-images/image-190.png)
![alt text](os-images/image-191.png)
![alt text](os-images/image-192.png)

# HOw scheduler can switch if the thread has come first time
![alt text](os-images/image-193.png)
![alt text](os-images/image-194.png)
![alt text](os-images/image-195.png)
![alt text](os-images/image-196.png)
![alt text](os-images/image-197.png)
![alt text](os-images/image-198.png)
![alt text](os-images/image-199.png)
![alt text](os-images/image-200.png)

# example
![alt text](os-images/image-201.png)

# Atomic
![alt text](os-images/image-202.png)
![alt text](os-images/image-203.png)

# Locks alterntive
![alt text](os-images/image-204.png)
![alt text](os-images/image-205.png)
![alt text](os-images/image-206.png)
Here in earlier the producer will get in deadlock beacuse it will acquire lock and go to infinte 
![alt text](os-images/image-207.png)
but it also has a problem means it will consume always cycles because lets say there is no consumers so it will acquire and release consuming cpu cycles called busy waiting 
![alt text](os-images/image-208.png)