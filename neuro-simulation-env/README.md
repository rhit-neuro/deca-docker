# neuro-simulation-env

AS OF MARCH 2021, THIS ENVIRONMENT IS DEPRECATED. Now that the simulation can also target CUDA, it is necessary to include the CUDA toolchain. Use the [cuda-neuro-simulation-env](../cuda-neuro-simulation-env/) for compilation instead.

## Features

This is the environment that you want to develop the code with. It has the toolchains for x86_64 and riscv64 built and ready to use.

If you are working on the unified x86_64/riscv64/CUDA codebase, use [cuda-neuro-simulation-env](../cuda-neuro-simulation-env/) instead. Due to certain changes to the build process to allow for CUDA compilation, this environment can no longer compile that codebase.

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
