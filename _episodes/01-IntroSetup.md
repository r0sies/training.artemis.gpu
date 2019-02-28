---
title: "Creating an environment for GPU computing"

author: "Nathaniel Butterworth, Cali Willet"

keypoints:
- GPU vs CPU
- CUDA
objectives:
- Understand why GPUs are cool
- Setting up a development environment
source: Rmd
teaching: 30
---


This episode introduces a few ways we can set up a working GPU environemnt. You will find to get a well-functioning CUDA development environment there is a precious balance between your operating system, your model of GPU, your NVIDIA GPU driver, and your CUDA version that straddle across all the other pieces (not to mention the software, e.g. tensorflow, python, keras, matlab, that depends on the underlying set-up).

## What is a GPU?

A Graphics Processing Unit as opposed to a Central Processing Unit (CPU).
Originally intended for sending an image to the pixels on the screen, someone then figured out that by treating data as a texture map you could perfom lots of calculations simultanously, and the age of the GPGPU (general-purpose graphics processing unit) began.

<figure>
  <img src="{{ page.root }}/fig/01_gpu.jpg" style="margin:10px;height:200px"/>
</figure><br>


## How do I get access to a GPU?

Your PC!

Sydney University HPC [Artemis](https://sydneyuni.atlassian.net/wiki/spaces/RC/pages/185827329/Artemis+User+Guide) 

Sydney University Virtual Research Desktop [Argus](https://sydneyuni.atlassian.net/wiki/spaces/RC/pages/212828220/Argus+User+Guide)

[NCI](http://nci.org.au/)

[Pawsey](https://pawsey.org.au/)

Other clouds like GCP, AWS, Azure, NGC, etc

### Why do I want to use a GPU?

<figure>
  <img src="{{ page.root }}/fig/01_gpufast.png" style="margin:10px;height:300px"/>
</figure><br>

We can visualise the CPU and GPU as something like this:
<figure>
  <img src="{{ page.root }}/fig/01_gpuVScpuGRID.JPG" style="margin:10px;height:300px"/>
</figure><br>

|CPU strengths| GPU strengths|
|---|---|
| Very large main memory | High bandwidth main memory |
| Very fast clock speeds | Latency tolerant via parallelism |
| Latency optimized via large caches | Significantly more compute resources |
| Small number of threads can run very quickly | High throughput |
| | High performance/watt |

|CPU weaknesses| GPU weaknesses|
|---|---|
| Relatively low memory bandwidth | Relatively low memory capacity |
| Low performance/watt | Low per-thread performance |

CPU strengths:
* Very large main memory
* Very fast clock speeds
* Latency optimized via large caches
* Small number of threads can run very quickly

CPU Weaknesses:
* Relatively low memory bandwidth
* Low performance/watt

GPU strengths: 
* High bandwidth main memory
* Latency tolerant via parallelism
* Significantly more compute resources
* High throughput
* High performance/watt

GPU weaknesses:
* Relatively low memory capacity
* Low per-thread performance


Threads/Blocks/all that.

<figure>
  <img src="{{ page.root }}/fig/01_gpuVScpu.png" style="margin:10px;height:400px"/>
  <img src="{{ page.root }}/fig/01_gpuVScpu2.png" style="margin:10px;height:400px"/>
  <figcaption> An informative way to compare CPU and GPU computing comparing speed and throughput.</figcaption>
</figure><br>


GPU devel environment and application examples


### How do you develop code for GPU computing?

The most common langauges for developing code for GPUs are
***CUDA***, ***OpenCL***, and ***OpenACC***. These are all low-level and require fairly strong programming capabilities. However, high-level languages like ***Python*** and ***Matlab*** and subsequent packages within them (keras, tensorflow, theano, etc), can make use of your GPU by essentially writing CUDA (or OpenCL) for you! We will see a few examples and you can decide what language best suits your use cases. We will be focusing on CUDA-capable cards (i.e NVIDIA). OpenCL works on the other most popular GPU card, AMD Radeons (Mac GPU of choice). Plus there has been a push from mobile markets to get more into the GPU space, so now companies like ARM and Intel (which also support OpenCL) are starting to have more of an impact on GPU computing. 



## Requirements

For HPC work all you need is an ssh client (instructions [here](./setup.html)).

### NVIDIA local installation instructions

**Windows 10**

Install [Visual Studio 2017](https://visualstudio.microsoft.com/).

Install the NVIDIA graphics driver and CUDA drivers.
Download both from the [NVIDIA download page](https://www.nvidia.com/Download/index.aspx?lang=en-us). 

Specific versions of tools working together for me are:

C compiler, installed with Visual Studio 2017, ***cl.exe***

```Microsoft (R) C/C++ Optimizing Compiler Version 19.16.27027.1 for x64```

Nvidia cuda compiler (installed with the CUDA toolkit), ***nvcc***

```nvcc: NVIDIA (R) Cuda compiler driver Cuda compilation tools, release 10.0, V10.0.130```


**Linux (Xubuntu 18.04)**

Probably as simple as selecting the NVIDIA driver.
Then installing the CUDA drivers for the driver/GPU combo.
More info here [https://informatics.sydney.edu.au/blogs/tf_on_linux/](https://informatics.sydney.edu.au/blogs/tf_on_linux/)

Specific versions of tools working together for me are:

C compiler, ***gcc***

```gcc (Ubuntu 6.5.0-2ubuntu1~18.04) 6.5.0 20181026```

and the Nvidia cuda compiler (installed with the CUDA toolkit), ***nvcc***

```nvcc release 9.0, V9.0.176```


**Mac OSX**

If you have Mac product newer than about 2014 you probably don't have CUDA-capable GPU card in there. This was done for various reasons. Nevertheless, there are still drivers from NVIDA, and a few options with external GPUs. But good luck, you are on your own. For now, you can do the Artemis examples!



### Which version(s) to use?

Depends what features you need; if you need the latest then go with that. 
Different cards have different compute capability and different CUDA requirements. And these options bleed down the dependency list (also known as software stack). So if you don't know, go for the latest stable release compatible over your software stack. Check your [CUDA compatability here](https://docs.nvidia.com/deploy/cuda-compatibility/index.html)


**There is an update for XXXX, should I get it?**
Maybe, but probably not. (Not while I am teaching you anyway.) This workshop is for scientific development of applications, chances are you will hack together some code and run it once, so we are not aiming to get this working on every GPU system in the world. But versioning is super important.




## What about Containers?
Docker/singularity are great for simplifying the development environments, BUT they still require the underlying installitions of NVIDIA drivers for your specific GPU card, plus a version of CUDA that works with that combo!






{% include links.md %}
