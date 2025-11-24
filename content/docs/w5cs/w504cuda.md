---
title: "CUDA"
description: ""
summary: ""
date: 2025-07-09T23:45:01+08:00
lastmod: 2025-07-09T23:45:01+08:00
weight: 504
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---


### Software Hierrarchial Architecture

| CUDA Parts | Samples | Description |
| - | - | - |
| CUDA Toolkit | NVCC (Compiler), profiler, debugger | Used for writing custom CUDA kernels or building pytorch (CUDA runtime and libraries) from source. Not necessary for running GPU applications. |
| CUDA Libraries | cuDNN (Conv, RNN, etc), cuBLAS (Linear Algebra), NCCL (Multi-GPU communication), cuFFT(Fast Fourier Transform), TensorRT | Provides high-level functionality to frameworka like PyTorch. The library will then compile to PTX/SASS. |
| CUDA Runtime (user space) | libcudart | Kernels provides device API to libraries and communicate with driver. |
| HOST NVIDIA Driver | `nvidia-smi` | Executes PTX/SASS from the runtime. Driver must be installed on the host for specific GPU. The CUDA driver version is backward compatible to CUDA runtime versiom. |

A pytorch with cuda is bundled with CUDA runtime, libraries, PTX kernels, architecture -specifc kernels. Except for NVIDIA driver. CUDA runtime and libraries must be bundled on the same version.

A docker image's CUDA runtime will call host os driver to use GPU.

PTX (Parallel Thread Execution) is the intermediate code that can run on multiple GPU architecture. SASS is the assembly code that is specific to a GPU architecture. SASS has better performance than PTX.

CUDA 11.x doesn’t include PTX operators or drivers for Blackwell architecture (sm_90). Hence, PTX is partially universal.

### Custom CUDA Kernels

```cpp
#include <stdio.h>

__global__ void vector_add(float *a, float *b, float *c, int n) {
    int idx = blockIdx.x * blockDim.x + threadIdx.x;
    if (idx < n) {
        c[idx] = a[idx] + b[idx];
    }
}

int main() {
    const int n = 100;
    float a[n], b[n], c[n];
    
    for (int i = 0; i < n; i++) {
        a[i] = i;
        b[i] = 2 * i;
    }

    float *d_a, *d_b, *d_c;
    cudaMalloc((void**)&d_a, n * sizeof(float));
    cudaMalloc((void**)&d_b, n * sizeof(float));
    cudaMalloc((void**)&d_c, n * sizeof(float));

    cudaMemcpy(d_a, a, n * sizeof(float), cudaMemcpyHostToDevice);
    cudaMemcpy(d_b, b, n * sizeof(float), cudaMemcpyHostToDevice);

    int threadsPerBlock = 32;
    int blocks = (n + threadsPerBlock - 1) / threadsPerBlock;
    vector_add<<<blocks, threadsPerBlock>>>(d_a, d_b, d_c, n);

    cudaMemcpy(c, d_c, n * sizeof(float), cudaMemcpyDeviceToHost);

    for (int i = 0; i < 10; i++)
        printf("%f\n", c[i]);

    cudaFree(d_a);
    cudaFree(d_b);
    cudaFree(d_c);
    return 0;
}
```

### CUDA Concepts

#### Units

| CUDA Parts | Description |
| - | - |
| Grid | A collection of blocks for one kernel launch |
| Block | Group of threads that can cooperate and share memory |
| Thread | A single execution unit in a block |

#### Memory

| Memory Type            | Scope          | Speed      | What It's For           |
| ---------------------- | -------------- | ---------- | ----------------------- |
| **Registers**          | per thread     | fastest    | local variables         |
| **Shared Memory**      | per block      | fast       | cooperative thread data |
| **Global Memory**      | all GPU        | slow-ish   | main working memory     |
| **Constant / Texture** | cached         | fast       | read-only data          |
| **Unified Memory**     | CPU-GPU shared | convenient | but slower              |

#### Concepts

- Functional Scope: vector add, matrix multiply
- Warp: group of 32 threads that execute in parallel. Avoid `if`, `while` divergent control flow which will make threads wait
- Memory Coalescing: access adjacent memory
- Synchronization
- SM (Multiple Stream Multiprocessor) executes blocks in parallel (The brain of GPU)
- Occupancy pressure: little threads are running per SM
- Register pressure: too many registers are used
