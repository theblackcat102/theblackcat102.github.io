---
keywords:
    - slurm
    - workload manager
comments: true
title: Slurm TLDR;
---

As hinted in the title, this is a short intro to slurm command.

### What the heck is slurm?

Slurm is workload manager, that help user to schedule resource from a high performance computing full of thousands of GPUs and CPUs.

Start using slurm in 5 steps:

You usually have a quota to how many resource you can use and will be given a authentication token ( or account number ).  All computing task need to start using bash scripts, hence if your code is python, you need to add using ```python run.py```

An example config of slurm is as follows:

```
#!/bin/bash
#SBATCH --ntasks <Your number of node allocate>
#SBATCH -A <Account Number>
#SBATCH -J <Job name>
#SBATCH -p <Node config>
#SBATCH --gres=gpu:<GPU number>
#SBATCH --cpus-per-task=<CPU number>
```

ntasks: You can view this is as the number of virtual machines

while gres, cpus-per-task controls the resource number of each virtual machine.

1. srun

```
srun your_batch_script.sh
```

Allocate the needed resource return all output stream to your terminal interactively.

2. sbatch

```
sbatch your_batch_script.sh
```

Allocate the needed resource and returns a job id. You can use scancel and squeue to kill or check the status of your job id.

3. scancel

```
scancel <your job id>
```

Kill your current running jobs

4. squeue

```
squeue --account=<Account id>
```

List all the currently active jobs.

### Some notes 

* If you are using GPUs always add ```nvidia-smi``` to your bash script to check whether the right amount of GPU resource is allocated.



