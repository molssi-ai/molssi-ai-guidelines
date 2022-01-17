.. _hpc_guidelines:

**********************************************************
MolSSI Guidelines on APOD Cyclic Parallelization Strategy
**********************************************************

* Source: |hpc_badge|

This document is based on NVIDIA's `CUDA C++ Best Practices Guide <https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html>`_
and presents a systematic cyclic strategy for parallelizing serial codes using CUDA toolkit.

Prerequisites
=============

This guide assumes the user is familiar with the (CUDA) C++ programming language and has access to CUDA-capable graphical 
processing units (GPUs) and an existing working serial code.


Systematic Acceleration Strategy
================================

The main focus of this guide is to present a four-step cycle to accelerate a sequential code for NVIDIA GPUs using CUDA C++. 
This cycle consists of **assessment**, **parallelization**, **optimization** and **deployment** (APOD). The APOD prioritizes
its recommendations based on their efficiency and scope i.e., actions that provide significant performance improvements have 
higher priorities. This prioritization allows programmers to benefit from incremental speedups as early as possible while making 
the changes to the code localized and evolutionary not revolutionary.

Assessment
----------

A systematic way to gain quantitative knowledge about your code and locate the bottlenecks in the execution time is using profilers
such as GNU's *gprof* as well as NVIDIA's *NSight Systems* and *Nsight Compute*. Loops are common targets for parallelization because
they perform a single instruction multiple times. After identifying hotspots in the code, one can set a theoretical upper bound for 
the expected speedups using `Amdahl's (strong scaling) <https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#strong-scaling-and-amdahls-law>`_ 
and/or `Gustafson's (weak scaling) <https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#weak-scaling-and-gustafsons-law>`_ 
laws.

Parallelization
---------------

Depending on the application and the nature of the target code sections identified in the previous step, there are three possible major 
tools that can be adopted for parallelization: (i) **parallel libraries**, (ii) **parallelizing compilers** and (iii) **custom codes**.

*Parallel Libraries*
^^^^^^^^^^^^^^^^^^^^

The explicit usage of parallel libraries (such as *Thrust*) or replacing  the existing libraries in the serial code with their parallel 
alternatives (such as switching from *BLAS* to *cuBLAS*) is probably the most convenient way to implement parallelization.

*Parallelizing Compilers*
^^^^^^^^^^^^^^^^^^^^^^^^^

Compiler directives such as *OpenMP* and *OpenACC* can also be employed to provide hints to the compilers for parallelizing specific sections
of the program and mapping the computations to the computing unit's architecture without modifying the underlying codes.

*Custom Codes*
^^^^^^^^^^^^^^

Whenever the existing functionality of the parallel libraries and compiler directives are not sufficient for the target programming purposes,
adopting parallel programming languages such as CUDA C/C++ or Data-Parallel C++ becomes necessary. Using these programming languages, the code 
hotspots can be refactored into kernels and launched on the accelerator architectures such as GPUs and field programmable gate arrays.

Optimization
------------

Parallel code optimization techniques improve the performance of the implemented code and allow for an early realization of the speedups from 
the parallelization step in the APOD cycle. In general, performance optimization involves three main techniques: (i) **maximizing parallelism**,
(ii) **maximizing memory bandwidth**, and (iii) **maximizing instruction bandwidth**.

*Maximizing Parallelism*
^^^^^^^^^^^^^^^^^^^^^^^^

According to Amdahl's law, one can improve the performance by exposing as much parallelism in the code as possible. After the parallelization
step, an efficient mapping of the algorithms and data structures to the accelerator hardware architecture is crucial. The maximum hardware 
occupancy is often desired and can be achieved by trial and error with documenting the performance of various execution configurations in the 
target kernel launch. High-level optimization techniques such as exposing concurrent execution on multiple device streams and maximizing the 
overlap between data transfer and computation are also necessary for performance improvement.

*Maximizing Memory Bandwidth*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to optimize the memory utilization, one should minimize the data transfer between the host and the device(s). Kernel's access to global
memory should also be minimized in favor of maximizing the usage of device's shared memory. Care must be taken for an optimal organization of memory
access patterns.

*Maximizing Instruction Bandwidth*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Low-throughput arithmetic instructions and thread warp divergence in control flows should be avoided for instruction optimization. Whenever possible,
single-precision computations should be employed (instead of double-precision) for a trade-off between the expected accuracy and performance.

Deployment
----------

Compute capabilities determine the features available on each generation of the accelerator devices. As such, in order to support all features 
available in the program and maximum performance optimization by the compiler, the source code should be compiled for the native compute compatibility
of the target GPU(s). For industrial applications in parallel environments, NVIDIA Management Library (NVML) and 
`cluster management tools <https://developer.nvidia.com/cluster-management>`_ can be employed to maximize efficiency and performance.

.. citation badges

.. |hpc_badge| image:: https://zenodo.org/badge/DOI/10.5281/zenodo.5866422.svg
   :target: https://doi.org/10.5281/zenodo.5866422


