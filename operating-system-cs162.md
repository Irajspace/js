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




   