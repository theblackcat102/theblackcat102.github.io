---
keywords:
  - experience
comments: true
title: Understanding how 2022 CPU works as noob
cover_image: 
---

CPU design is complex as shit in today world and looks nothing like what I learned in computing architecture back when I was in school. In the past few months I read some good articles and wanted to write some of my understanding down.

### A basic understanding of simple CPU

So what a CPU does is do calculation : addition and moving data around. So in order to tell the CPU what to do, you need a set of rules and format to follow so everyone can follow.

> I try to be simple and skip something here because I need to spent the time on modern CPU design

## Instruction

Suppose you have some input store somewhere with the address of that data and you want to do an operation on these data ( addition, subtraction, division, move to other address ). You need to write these command.

So this is where instruction come to play.

![Sample of instruction of ARM](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/Introduction_to_ARM_Assembly3.png)
[source](https://www.allaboutcircuits.com/technical-articles/how-to-write-assembly-basic-assembly-instructions-ARM-instruction-set/)


As of the 2022 modern world, we had x86 (CISC), ARM (RISC) making up the majority of CPU we use.

## Arithmetic logic unit (ALU)

![ALU from wikipedia](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/330px-ALU_block.gif)


Once you know the instruction, a CPU can now parse these instruction and pass it to an ALU to do calculation. An ALU basically takes care of the addition, subtraction... all the math operations. 


## Execution Pipeline

So you have a instruction you wish to run, what steps are you going to do?

The steps of a CPU instruction can be broken down into the following phases:

    Fetch: The CPU retrieves the next instruction to be executed from memory.

    Decode: The CPU decodes the instruction to determine what operation it specifies.

    Execute: The CPU carries out the operation specified by the instruction.

    Store: The CPU stores the result of the operation in memory or in a register.

These steps are typically performed in a repeating cycle known as the fetch-decode-execute cycle, which allows the CPU to continuously execute instructions and perform operations on data. The speed at which the CPU can perform this cycle is known as the clock speed, and is measured in hertz (Hz). The faster the clock speed, the more instructions the CPU can execute per second.

However we doesn't want to do only math function, we also want to do series of functions sometimes repeatedly. So we had Accumulator, that is used to hold the result of arithmetic and logic operations performed by the CPU. In most cases, the accumulator is a register that is used to store the result of an operation performed on data from memory or from another register. The accumulator is an important part of the CPU because it allows the CPU to perform a wide range of operations on data without having to constantly read and write to memory, which would slow down the computer's performance.

## Microcode engine (decoder)

As CPU design became more complex, the control logic for executing an instruction started becoming more complex and bigger. Hence microcode design was proposed to act as a abstraction between instruction and machine pipeline execution. Microcode optimization has since be one of the key optimization in many Intel CPU releases since 8086 (1978).

In modern CPU, the microcode is what drives the decoder section inside the CPU.


And here's a i7-6700K die shot:

In modern CPU, the microcode is what drives the decoder section inside the CPU.
 | And here's a i7-6700K die shot:

<p float="center">
  <img src="https://hackaday.com/wp-content/uploads/2017/12/microcodemp4download-shot0002_thumbnail-themed.jpg?resize=400,381" width="40%" />
  <img src="https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/main-qimg-cce3ba853e67deb340000ccf7816510c-pjlq.jpg" width="25%" /> 
</p>

On the left, the microcode is what drives the decoder section inside the CPU ([source](https://hackaday.com/2017/12/28/34c3-hacking-into-a-cpus-microcode/)). While on the right is a [i7-6700K die shot](https://www.quora.com/Why-does-a-core-i7-have-1-5-B-transistors-and-486-just-1-5m), the microcode engine is highlighted in red rectangle.


## Modern tricks that make your CPU fast

As you might have notice, a more modern CPU doesn't look like this ([source](http://www.righto.com/2016/12/die-photos-and-analysis-of_24.html)) 8008 CPU by Intel in 1983.

![8008 die shot](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/8008-die-block-diagram.png)

But this ([source](https://www.reddit.com/r/intel/comments/qhbbow/10nm_esf_intel_7_alder_lake_die_shot/))

![Alder lake die shot](https://preview.redd.it/lyhmdzo6c3w71.jpg?width=960&crop=smart&auto=webp&s=89fa3a1cf9d1925bb5f4922333e9c902e7c75148)

Much have changed since the 21st century and I will elaborate some of the major changes that shape our modern CPUs.

Do note what I am showing here is only the tip of an iceberg and are only those which I think is pretty important. If you wish to go down the rabbit hole here's some keyword that can kept you busy : NUMA topology, big LITTLE, Re-order buffer.

### Multi thread

Multithreading is a technique used by computer systems to improve the performance of certain types of applications. It involves allowing a single CPU, or central processing unit, to execute multiple threads of execution concurrently. Each thread represents a separate sequence of instructions that can be executed independently of the other threads. By executing multiple threads concurrently, the CPU can improve its overall performance and make more efficient use of its resources. This is because it can switch between threads whenever one thread is waiting for input or output, allowing it to continue executing useful work even when some threads are idle.

### SMT

SMT, or simultaneous multithreading, is a variant of multithreading that allows each physical CPU core to execute multiple threads simultaneously, rather than just one thread per core as in traditional multithreading. This allows the CPU to make more efficient use of its resources and improve its overall performance by allowing more work to be done in parallel. SMT is often used in applications that need to perform multiple tasks concurrently, such as web servers and media players.

Both multithreading and SMT are important techniques for improving the performance of modern computer systems, and they are used in a wide range of applications. These techniques allow CPUs to execute more instructions in parallel, which can improve the overall speed and efficiency of the system.

### Branch predictor

Branch instructions are a type of instruction that can cause the CPU to branch to a different part of the program and execute a different sequence of instructions depending on the result of a conditional test. For example, a branch instruction might be used to check if a number is greater than zero, and if it is, the CPU will branch to a different part of the program to execute a different set of instructions. Branch predictors are used to improve the performance of the CPU by predicting the outcome of branch instructions and speculatively executing the appropriate instructions before the result of the branch is known for sure. 

TLDR; you predict the outcome of the branch (where do your instruction jump to next, for example : if-else logic ) in order to execute the branched instruction section. If your predictions are incorrect, you need to fallback and execute the correct instruction. 

This allows the CPU to avoid stalling and continue executing useful work while it waits for the result of the branch instruction.

#### Speculative execution

Following the jazz of branch predictor, we can also predict what instruction you will need to execute next and run it first. If the prediction turns out to be correct, the results of the speculative execution can be used immediately, which can improve the overall performance of the CPU. If the prediction is incorrect, the results of the speculative execution are discarded and the correct instructions are executed instead. Speculative execution is a complex and highly optimized process that is essential to the performance of modern CPUs.



### Tiered cache

One unsung hero of double digit improvements over generations in CPU/GPU since 2019 must be the cache size increase. 

Once CPU/GPU started became very efficient at number crunching, they will soon bottleneck by how fast the memory can kept them fully ultized. This is where tiered cache such as L0, L1, L2, L3 cache came into play. By storing some frequently accessed data and instructions near the ALUs, the idle time can be reduced significantly. 


|   | Previous generation  | New generation  |  Improvements* |
|---|---|---|---|
| Nvidia 90 series  | L2 6MB (3090)  | L2 72MB  (4090)  |  42% |
| Intel i9  | 30MB (12900k)  |  37MB (13900k) | 13%  |
| AMD ryzen 8  | 32MB (5800X) | 96MB (5800X3D) | 15%  |
| Apple M1 series  | 16MB (M1) | 48MB (M1 Max) | 0-1%  |

Improvements varies by benchmark and cannot be compared across different compute from different designs; single core benchmarks are taken for CPU.



#### Footnote:

This article is cowritten by ChatGPT in small sections to speed up my narrative writings. ChatGPT does not guide any of my writing direction and opinions.