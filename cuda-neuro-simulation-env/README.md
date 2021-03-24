# cuda-neuro-simulation-env

Dynamically-linked x86_64 binaries built with this environment (i.e., using `-DCMAKE_BUILD_TYPE=Debug`) should usually be run inside this environment. Binaries containing CUDA cannot run inside this environment. RISC-V binaries can only run on RISC-V systems, such as the Rocket Chip.

## Features

This is the environment that you want to develop the code with. It has the toolchains for x86_64, riscv64, and CUDA 10.2 built and ready to use.

Use this environment if you are working on the unified x86_64/riscv64/CUDA codebase, whether you are working on CUDA directly or not. Currently, this is the `cuda` branch of the `fixed-neuro-sim` repository.

Even if you are not working on the unified codebase, we recommended that you use this image. It has several improvements over the regular [neuro-simulation-env](../neuro-simulation-env/), and can compile for any of the existing simulation targets. The neuro-simulation-env environment cannot compile the unifide codebase for any targets.

## Running for the first time

Download this docker image with:

```bash
docker pull rhitdeca/cuda-neuro-simulation-env
```

Start your container for the first time with:

```bash
# Run this from where you cloned the fixed-neuro-simulation repo
# e.g. ~/fixed-neuro-simulation
docker run -it -v $(pwd):/project --name cnsenv rhitdeca/cuda-neuro-simulation-env:latest bash
```

* `-it` - creates an interactive terminal for you to type commands into.
* `--name cnsenv` - names this container `cnsenv`.
* `-v $(pwd):/project` - mounts the current directory on your host computer to `/project` in this container.

## Running subsequent times

See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building

To build this image, run the following command:

```bash
# cd into this folder first
cd cuda-neuro-simulation-env
# Make sure to replace <version> with your version number for the image you're building
docker build . -t rhitdeca/cuda-neuro-simulation-env:<version>
```

It's probably easier to just download it from Docker Hub.
