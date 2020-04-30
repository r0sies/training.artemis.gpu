---
title: "Writing and running your first GPU program"

keypoints:
- Compilation of C and CUDA code are siilar
- Running serial code and GPU code is similar

objectives:
- Compile and run our first code

teaching: 10
exercises: 10
questions:
- What compiler can you use to build C code?
- What compiler can you use to build CUDA code?

source: Rmd

---

## Hello World

Make a new text file called ```hello_world.c``` as follows:


```
#include <stdio.h>

void hello_world_kernel()
{
    printf("Hello World!\n");
}

int main()
{
    hello_world_kernel();
}
```
Save it and compile your C code with:

```gcc hello_world.c -o hello_cpu```

Now run your compiled program and get the expected output...
```
./hello_cpu
Hello World!
```

Great, so it is running as expected on CPU, now lets do it on the GPU. Make a new text file called ```hello_world.cu```:

```
#include <stdio.h>

__global__ void hello_world_kernel()
{
    printf("Hello GPU World!\n");
}

int main()
{
    hello_world_kernel <<<1,8>>>();
    cudaDeviceReset();
}
```
What are the key differences here?

Now compile your GPU code with the CUDA compiler, nvcc,

```nvcc hello_world.cu -o hello_gpu```

Run your compile CUDA code and get the expected GPU output...

```
./hello_gpu
Hello GPU World!
Hello GPU World!
Hello GPU World!
Hello GPU World!
Hello GPU World!
Hello GPU World!
Hello GPU World!
Hello GPU World!
```

Great, so that is a very simplified example of building and executing some basic CUDA code. These fundamentals are similar for compiling any code, and for executing any program.

Okay now let's take it to Artemis.



{% include links.md %}
