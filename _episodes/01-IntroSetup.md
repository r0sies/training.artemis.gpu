---
title: "Intro to GPU computing"

author: "Nathaniel Butterworth, Cali Willet"

keypoints:
- GPU vs CPU
- Suitable problems for GPU
- CUDA, and high level GPU environments
- Where to get one

objectives:
- Understand why GPUs are cool
- Setting up a development environment

teaching: 30
exercises: 0
questions:
- What is a GPU?
- How do I get access to a GPU?
- GPU or CPU?
- How do I develop code for GPU computing?

source: Rmd

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



<figure>
  <img src="{{ page.root }}/fig/01_gpuVScpu.png" style="margin:10px;height:400px"/>
  <img src="{{ page.root }}/fig/01_gpuVScpu2.png" style="margin:10px;height:400px"/>
  <figcaption> An informative way to compare CPU and GPU computing comparing speed and throughput.</figcaption>
</figure><br>

#### Some keywords

A ***thread*** is like a single computational task or instruction or kernel that is run on the GPU (or CPU).

A ***thread block*** is a group of threads in the same location on the GPU so they can communicate easily with each other.

A ***grid*** is the collection of thread blocks.

When executing your kernel (i.e. function), the typical CUDA command looks like this:

```
//The numbers possible here are dependent on your GPU hardware.
YourKernel<<<NumberOfBlocks,NumberOfThreadsPerBlock>>>(...) 
```

<figure>
  <img src="{{ page.root }}/fig/01_threads.png" style="margin:10px;height:400px"/>
</figure><br>

Use device query (or gpuQuerey in Matlab) to see some details about your GPU.

<figure>
  <img src="{{ page.root }}/fig/01_gpuenv.jpg" style="margin:10px;height:400px"/>
  <figcaption> Many different ways to use and interface GPUs.</figcaption>
</figure><br>


Having proposed GPU (or CPU) compute time on grant applications can show you are conducting accelerated research! Get in touch with us for help estimating your resource usage, or for any assitance, [https://informatics.sydney.edu.au/](https://www.sydney.edu.au/research/facilities/sydney-informatics-hub.html)


### How do you develop code for GPU computing?

The most common langauges for developing code for GPUs are
***CUDA***, ***OpenCL***, and ***OpenACC***. These are all low-level and require fairly strong programming capabilities. However, high-level languages like ***Python*** and ***Matlab*** and subsequent packages within them (keras, tensorflow, theano, etc), can make use of your GPU by essentially writing CUDA (or OpenCL) for you! 

We will see a few examples and you can decide what language best suits your use cases. We will be focusing on CUDA-capable cards (i.e NVIDIA). OpenCL works on the other most popular GPU card, AMD Radeons (Mac GPU of choice). Plus there has been a push from mobile markets to get more into the GPU space, so now companies like ARM and Intel (which also support OpenCL) are starting to have more of an impact on GPU computing. 


{% include links.md %}
