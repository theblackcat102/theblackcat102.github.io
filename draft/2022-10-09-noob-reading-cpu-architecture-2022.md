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

### Multi thread


### Branch predictor


#### Speculative execution



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