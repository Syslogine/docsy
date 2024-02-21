---
linktitle: "Install CUDA Toolkit"
title: "How to install CUDA toolkit from Ubuntu Repository"
weight: 2
tags: ["how to", "install", "cuda", "toolkit", "ubuntu", "repository"]
categories: ["Ubuntu"]



description: >
  Simple tutotial for how to install CUDA toolkit from Ubuntu Repository
---

Although you might not end up witht he latest CUDA toolkit version, the easiest way to install CUDA on Ubuntu 20.04 is to perform the installation from Ubuntu's standard repositories.

To install CUDA execute the following commands:
```bash
sudo apt update &&\
sudo apt install nvidia-cuda-toolkit
```

All should be ready now. Check your CUDA version:
```bash
nvcc --version
```
```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Sun_Jul_28_19:07:16_PDT_2019
Cuda compilation tools, release 10.1, V10.1.243
```
