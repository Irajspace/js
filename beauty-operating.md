# Operating System

## What does an Operating System do?

- Memory Management  
- I/O Management  
- CPU Scheduling  
- Multitasking / Multiprogramming  

---

## The only thing running at all times is kernel

![alt text](image.png)

---

## What makes something a system

- There is a connection between interrelated parts → complexity is O(n²)  
- To overcome this, we use APIs to reduce complexity  

---

## Hardware and software

- There are registers in processors which point to parts of memory that allow the program to run  
- In between there may be caches that make the system fast  
- Then there is page table and TLB that make virtual memory  
- The OS abstracts hardware details from the application  

![alt text](image-1.png)

---

## Abstraction
 
- We are creating an abstraction of hardware  

Examples:
- Processor → threads  
- Memory → address spaces  
- Storage → files  
- Networks → sockets  

- A process can run using all these abstracted details  

- Above this, there is another layer of abstraction called system libraries / security libraries (e.g., SSL)  

![alt text](image-2.png)

- Each process runs independently and gives isolation  

![alt text](image-3.png)

- System libraries are linked into our program → compiled → executed by processes  

---

# Process

![alt text](image-4.png)  
![alt text](image-5.png)

---

# The illusion of multiple processors

- We switch between processes so fast that it looks like we have multiple processors  
- Registers point to where execution left off  

![alt text](image-6.png)  
![alt text](image-7.png)

---

# Abstraction

![alt text](image-8.png)  
![alt text](image-9.png)  
![alt text](image-10.png)

---

# Instruction cycle

- Program counter (PC) points to memory  
- CPU:
  - Fetch  
  - Decode  
  - Execute  

---

## Thread

- Has its own:
  - Program counter  
  - Registers  
  - Execution flags  
  - Stack  

![alt text](image-11.png)  
![alt text](image-12.png)  
![alt text](image-13.png)

- Execution state is stored in registers and memory (TCB → Thread Control Block)  

![alt text](image-14.png)  
![alt text](image-15.png)  
![alt text](image-16.png)

---

## Address Space

![alt text](image-17.png)

- Heap → allocated using `malloc`  

![alt text](image-18.png)

---

## Protection

![alt text](image-19.png)  
![alt text](image-20.png)

- Base and bound:
  - address ≥ base  
  - address < bound  

---

### Address space translation

![alt text](image-21.png)  
![alt text](image-22.png)

- Page tables convert virtual addresses → physical  

---

## Process

![alt text](image-23.png)

### Tradeoff

![alt text](image-24.png)

---

## Multithreading or single-threading

![alt text](image-25.png)  
![alt text](image-26.png)  
![alt text](image-27.png)

- Process = container  
- Thread = execution element  

---

## Why do we need processes

![alt text](image-28.png)

---

## Fourth OS concept

![alt text](image-29.png)  
![alt text](image-31.png)  
![alt text](image-32.png)

- In system mode, base and bound are ignored  

---

## Switching to kernel mode

![alt text](image-33.png)

- Interrupt table is loaded at boot  
- Used to switch between processes  

![alt text](image-34.png)  
![alt text](image-35.png)  
![alt text](image-36.png)

---

## Memory management

![alt text](image-37.png)  
![alt text](image-38.png)

---

## Adding Thread

![alt text](image-39.png)  
![alt text](image-40.png)

- Threads interleave execution  

---

## Facts

![alt text](image-41.png)

---

## Switching

- In 2nd case, blockage due to I/O → cannot interleave  

![alt text](image-42.png)  
![alt text](image-43.png)

- Threads share same address space  

![alt text](image-44.png)

---

## Clarification

![alt text](image-45.png)  
![alt text](image-46.png)

---

## POSIX threads

![alt text](image-47.png)

---

# Thread function explanation

- Start routine → pointer to function  
  - takes `void *`  
  - returns `void *`  

- Thread join:
  - waits until thread completes  

![alt text](image-49.png)

- Trap instruction:
  - switches to kernel mode  
  - wrapper around system call  

![alt text](image-50.png)

- Parent continues only after all threads finish  

![alt text](image-51.png)

---

## Command-line arguments

Example:
```bash
./program.out 5