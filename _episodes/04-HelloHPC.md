---
title: "Running on HPC"
teaching: 10
exercises: 10
questions:
- "How do you set up your folder structure?"
- "How do you compile on Artemis?"
objectives:
- "Learn how to compile and run code on HPC."
keypoints:
- "Copy relevant files to directories."
- "Load modules and compile code."
- "Submit jobs to the scheduler."
---

You have connected to Artemis, great! Now let's get all the bits of code in a folder we can use:

```
cd /project/Training
mkdir <yourname>
cd <yourname>
cp /project/Training/GPUtraining/* .
```

Printing your current working driectory with, ```pwd```, will ensure you are in the correct directory.
~~~
/project/Training/nathan
~~~

And listing the files with ```ls```, will ensure you have the correct files.
~~~
gpu_demo_Mandelbrot.m  hello_world.cu  runv100.pbs             timeseries.py
hello.pbs              runk40.pbs      sydney_temperature.csv
hello_world.c          runMatlab.pbs   timeseries.ipynb
~~~

Great, we are ready to compile our code.


## Compile on Artemis HPC
You will need to either copy or re-write your programs on the remote computer, Artemis. We then have to compile the program again becasue the hardware on Artemis is probably different to what is on your local machine. Generally (and for optimal performance) you will have to compile your software on any different computer (e.g. Artemis @ USYD, GADI @ NCI, MAgnus @ Pawsey, AWS, etc) you want to run it on.
The compiling method is the same, but we need to make sure we load the required programs, then the procedure is the same.

```
#First load the cuda module - this gives us access to nvcc
module load cuda/8.0.44

#Then compile as before
nvcc hello_world.cu -o hello_gpu
```

Now, if you have tried to run it, you will find that you will get no output - that is because you are on a ***login node***, i.e. there is no GPU there. If you want to use a GPU you must run your code on a gpu node!
There is one on the training node we are using today to speed things up. And there are several more you can access normally on the production nodes.

***Note***: Some codes require significant amounts of RAM and can take a long time to compile. If that is the case, use an interactive job or submit the compilation steps to the queue!.

Let's write a pbs script to get our code running, create or edit the file called ```hello.pbs```
```
#! /bin/bash

#PBS -P Training
#PBS -N hwGPU 
#PBS -l select=1:ncpus=1:mem=1gb:ngpus=1
#PBS -l walltime=00:01:00
#PBS -q defaultQ

#Change into the directory where you submitted qsub
cd $PBS_O_WORKDIR

#Load modules we need
module load cuda/8.0.44

#Actually run the program
./hello_gpu

```
And submit the jobscript to the queue with 
```
qsub hello.pbs
```
This submits your job to the Artemis queue with the resources you have requested. It then runs the commands in the script, so will eventually run our ```hello_gpu``` program. Wait a couple minutes for the code to run and complete (you can check your position in the queue with ```qstat```.)

Now when it has finished, check the output in **hwGPU.o???**
Is it what we expect!? 
You can have a look at the **hwGPU.e???** file to see if any messages were sent to the error log. These can be warnings, or if somehitng has gone wrong (like if you make a typo and Artemis can't find the files you are expecting) then hopefully a useful message has appear in this log. 
Finally, check out the **hwGPU.o???_usage** file for a detailed look at all the resources your code used.







{% include links.md %}
