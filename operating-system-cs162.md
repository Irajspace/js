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
   