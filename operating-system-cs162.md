# Operating System

## What does an Operating System do?

- Memory Management  
- I/O Management  
- CPU Scheduling  
- Multitasking / Multiprogramming  

## The only thing running at all times is kernel

![alt text](image.png)

## What makes something a system

- There is a connection with each interrelated parts means there is complexity of o(n2)
To overcome this one has to come up with apis to level down this complexity

## Hardware and software

- There are registers on processors which pointing to parts of memory that allows the program to run. In between there may be caches that make system fast 
Then there is page table and TLB that make virtual memory 
The OS abstracts these abstracts the hardware details from the application
![alt text](image-1.png)


## Abstraction
 
- We are creating a abstraction of hardware
 like for processor-threads, memory-address spaces,storage-files, networks-sockets

 that process can run all these abstracted details

 - Above this there is another layer of abstraction called system libs ,security libs which allow you to do ssl on
 ![alt text](image-2.png)

 Each processes are running at a time and each give isolation to each other
 ![alt text](image-3.png)
 here you can see system libraries are linked into our program which is later converted into bits by compiler and then run by processes
 
 # Process
 ![alt text](image-4.png)
 ![alt text](image-5.png)

 # The illusion of multiple processors

 - Here what we do is we try to switch alternate between the two processes so fast we thought we are having two processors. the registers are pointing towards green or brown memory where it is left off
 ![alt text](image-6.png)
 ![alt text](image-7.png)

 # Abstraction
 ![alt text](image-8.png)
 ![alt text](image-9.png)
 ![alt text](image-10.png)

# Instruction cycle
- So what happens is program counter present at processor points to memory allow the processor to have set of instructions . It pulls the instructions in from the memory and decode it and then we execute it

Now under this 

## Thread
  It got its own program counter, registers,execution flags, memory stack
  ![alt text](image-11.png)
  ![alt text](image-12.png)
  ![alt text](image-13.png)
  A CPU has registers, including the Program Counter (PC), which points to the next instruction in memory. The CPU fetches that instruction, decodes it, and executes it. The thread’s execution state (context) is partly stored in registers and partly in memory.(TCB-> thread control block)
  ![alt text](image-14.png)
  ![alt text](image-15.png)
  ![alt text](image-16.png)

## Address Space
   ![alt text](image-17.png)
   whats in heap segment ->things allocated with malloc
   ![alt text](image-18.png)

## Protection
   How OS can protect
   ![alt text](image-19.png)
   ![alt text](image-20.png)
   - With base and bound it is like hardware type check means the address space should be greater than base and it should be less than bound

   Adress space translation
   ![alt text](image-21.png)
   ![alt text](image-22.png)
    - Page tables is used to convert virtual address into physical ones

## PRocess
 ![alt text](image-23.png)
 Tradeoff-
 ![alt text](image-24.png)

## Multithreading or single-threading
 ![alt text](image-25.png)
 ![alt text](image-26.png)

![alt text](image-27.png)
process is a container and thread is an execution element

## Why do we need processes
 ![alt text](image-28.png)

## Fourth OS concept
  ![alt text](image-29.png)
  ![alt text](image-31.png)
  ![alt text](image-32.png)
  in system mode base and bound is ignored because we have full spaces

  These are the ways we can go from user mode to kernel mode
  ![alt text](image-33.png)
  - This interrupt table is already loaded in os boots and run the execution that whether to switch from process a to process b
  ![alt text](image-34.png)
![alt text](image-35.png)
![alt text](image-36.png)

## MEMORY management
![alt text](image-37.png)
![alt text](image-38.png)

## Adding Thread
![alt text](image-39.png)
![alt text](image-40.png)
Here one can interlave between threads mean one can go and leave and do other job

## Facts
![alt text](image-41.png)

## Switching
Here in 2nd case there is blockage due to I/O operation that is the reason it cant interleave between threads
![alt text](image-42.png)
![alt text](image-43.png)
- In multithreaded processes, one can share data betweensame adresses ... means same processes

![alt text](image-44.png)

Clearance
![alt text](image-45.png)
![alt text](image-46.png)

posix threads
![alt text](image-47.png)

# The way we can read this is go from inside to out star routine is a pointer to a function that takes a void * and return a void *
 - Thread join means until thread is not completed it will not go 
![alt text](image-49.png)
special trap instruction lets you jump from user mode to kernel mode and find out it is not error it is used to create thread and this is wrapper around system call
![alt text](image-50.png)
You see this means until and unless all thread is not completed till finally then only parent thread will continue

![alt text](image-51.png)

- The first argument is no of arguments passed 
Lets take an example ./program.out 5 
here no of arguments passed is 2 
arg[0]="./program.out
arg[1]="5"

So basically what is happening is we are taking no of threads we want to create if we dont pass we are taking default as 2 
Then what are we doing is we are creating threads and joining as a parent thread

![alt text](image-52.png)
It is going to look like this
Here you can see the thread is not having same exact order
means it is not sequential because it got interleaved
![alt text](image-53.png)
Here pink stack grows long it can cause error in bluse stack
![alt text](image-54.png)

# INTERLEAVING AND INDETERMINSM
illusion is all threads run in a processes run but actually some of the run and some dont
![alt text](image-56.png)
![alt text](image-55.png)
![alt text](image-57.png)
![alt text](image-58.png)
Here you can see racing conditions happens
Although in Js 
we are it is single threaded it causes racing condition because of async code

![alt text](image-60.png)
![alt text](image-59.png)

## Threads cant share stack 
- beacuse is stack we have state stored
![alt text](image-61.png)
SOlution
![alt text](image-62.png)

# LOCKS
![alt text](image-63.png)
![alt text](image-64.png)

# How are we gonna lock it
![alt text](image-65.png)
![alt text](image-66.png)

# How are the processes start
![alt text](image-67.png)

![alt text](image-68.png)it
![alt text](image-69.png)
fork creates a process
it copies a process into another adr  ess space 
![alt text](image-70.png)
![alt text](image-71.png)
![alt text](image-72.png)
![alt text](image-73.png)
![alt text](image-74.png)

# Fork race
![alt text](image-75.png)
this is how new program is created Here what happended throw all my adress spaces and creates a new program means execute new instrucitons
![alt text](image-77.png)
![alt text](image-76.png)
![alt text](image-78.png)

# SEMAPHORES
- Here you can see if there is some critical section means lock have to be applied before this code
- One can do Sempahore down means now value =1 and now if any other tries to get in means it will change semaphore value to zero 
so it will not let to do it
![alt text](image-79.png)
![alt text](image-81.png)
![alt text](image-82.png)
![alt text](image-83.png)

# SHARE HEAP BUT NOT STACK
![alt text](image-84.png)
![alt text](image-85.png)
sleep(1)-> pauses this thread for 1 second

# Starting a new program
![alt text](image-86.png)

# SIgnalling
![alt text](image-87.png)

So what happens is this will loop infinite until a signal comes if it comes it will take and exit
![alt text](image-88.png)
![alt text](image-89.png)

# FILES
![alt text](image-90.png)
![alt text](image-91.png)
![alt text](image-92.png)
![alt text](image-93.png)

WITH THE STDIN AND STDOUT ONE CAN REDIRECT TO ANYOTTHER FILE
![alt text](image-94.png)
![alt text](image-95.png)
Reason for int
![alt text](image-96.png)

Earlier we were taking char by char now we take in buffer
![alt text](image-97.png)
![alt text](image-98.png)

# Design patterns
![alt text](image-99.png)
![alt text](image-100.png)
![alt text](image-101.png)

4 th lecture again 

![alt text](image-102.png)
![alt text](image-103.png)
![alt text](image-104.png)

# What will be the output difference
![alt text](image-105.png)
YOu will see that after 10 seconds only everything will be outputed 
it stores in the buffer or until and unless new line is not there
![alt text](image-106.png)
![alt text](image-107.png)
![alt text](image-108.png)

![alt text](image-109.png)

# What can happen if buffer didnt get flushed
![alt text](image-110.png)
![alt text](image-111.png)
![alt text](image-112.png)
# this is the solution Write flush after buffering so that it writs on disk
![alt text](image-113.png)
![alt text](image-114.png)

![alt text](image-115.png)
# WHy do we need sys calls less
![alt text](image-116.png)
![alt text](image-117.png)
![alt text](image-119.png)
![alt text](image-118.png)
![alt text](image-120.png)
![alt text](image-121.png)

# Fork in a multi-threaded process
![alt text](image-122.png)
![alt text](image-123.png)
![alt text](image-124.png)
![alt text](image-125.png)

# IPC AND SOKCETS
![alt text](image-126.png)

# THe network Req cycle
![alt text](image-127.png)
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
![alt text](image-128.png)

# Communication between process

- Process abstraction is designed to discourage inter-process communication
See here how process protects from each other
![alt text](image-129.png)
![alt text](image-130.png)

Why sharing data from data is expensive - beacuse everytime you have to read and write from disk
so forking for communication is expensive
- writing to file descriptor and reading from it

![alt text](image-131.png)

SOlution-
YOu can have shared data as as a space
![alt text](image-132.png)
![alt text](image-133.png)
   ![alt text](image-134.png)
   ![alt text](image-135.png)
   ![alt text](image-136.png)
   ![alt text](image-137.png)
   ![alt text](image-138.png)
   ![alt text](image-139.png)
   ![alt text](image-140.png)
   ![alt text](image-141.png)
   pipe is not a process its just a queue inside process
   ![alt text](image-142.png)
   Why does parent allow write and child allows read only explain
   ![alt text](image-143.png)
   ![alt text](image-144.png)
   ![alt text](image-145.png)
   ![alt text](image-146.png)

# EOF
![alt text](image-147.png)

# RPC
![alt text](image-148.png)

# How does sever knows about diff clients
- Ip address+port+protocol- makes communication channel unique
socket is a data structure including a queue
![alt text](image-149.png)

# Communication
![alt text](image-150.png)

# protocol of tcp/ip
- sequential order (data packets)
![alt text](image-151.png)
![alt text](image-152.png)
![alt text](image-153.png)
![alt text](image-154.png)
![alt text](image-155.png)
![alt text](image-156.png)
Socket protocol
![alt text](image-157.png)
Here child only listens to read and write and dont take new client whereas parent socket is responseible for listening new client
![alt text](image-158.png)

# Concurrent sockets
if you remove wait from parent this will become concurrent
![alt text](image-159.png)

# creating address
![alt text](image-160.png)
![alt text](image-161.png)
# sockets without protection
![alt text](image-162.png)
![alt text](image-163.png)
![alt text](image-164.png)
![alt text](image-165.png)
![alt text](image-166.png)
![alt text](image-167.png)

