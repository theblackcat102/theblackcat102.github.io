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


## Other important mechanism


However we doesn't want to do only math function, we also want to do series of functions sometimes repeatedly. So we had Accumulator, 


