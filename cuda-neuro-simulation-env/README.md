# cuda-neuro-simulation-env

## Features

This is the environment that you want to develop the code with.

It has the toolchains for `x86_64`, `riscv64`, and `CUDA 10.2` built and ready to use.

If you are not developing with CUDA, consider using regular `neuro-simulation-env` instead. It is a smaller image that does not contain the CUDA toolchain.

## Running for the first time

Download this docker image with:

```bash
docker pull rhitdeca/cuda-neuro-simulation-env
```

Start your container for the first time with:

```bash
# Run this from where you cloned the parallel-neuro-simulation repo
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
