# neuro-simulation-env

## Features
This is the environment that you want to develop the code with. It has the toolchains for x86_64 and riscv64 built and ready to use.

If you are working on the CUDA implementation of the simulation, use [cuda-neuro-simulation-env](../cuda-neuro-simulation-env/) instead. It is a much larger image, but contains all dependencies required for compiling the existing codebase with CUDA.

## Running for the first time
Download this docker image with:
```bash
docker pull rhitdeca/neuro-simulation-env
```

Start your container for the first time with:
```bash
# <parallel-neuro-simulation repo location> is where you cloned the parallel-neuro-simulation repo
docker run -it -v <parallel-neuro-simulation repo location>:/project --name nsenv rhitdeca/neuro-simulation-env:latest bash
```
* `-it` - creates an interactive terminal for you to type commands into.
* `--name nsenv` - names this container `nsenv`.
* `-v <parallel-neuro-simulation repo location>:/project` - mounts `<parallel-neuro-simulation repo location>` on your host computer to `/project` in this container.

## Running subsequent times
See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building
To build this image, run the following command:
```bash
# cd into this folder first
# Make sure to replace <version> with your version number for the image you're building
docker build . -t rhitdeca/neuro-simulation-env:<version>
```
