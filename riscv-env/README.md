# riscv-env

## Features
This docker image has `riscv-tools` installed and is the base image for `rocket-chip-env`, `neuro-simulation-env`, and `firesim-software-env`.

## Running for the first time
You shouldn't need to use this image on it's own, it's intended to be used as the base image for other images that need `riscv-tools`. However, you can use this image on it's own if you want to.
Download this docker image with:
```bash
docker pull rhitdeca/riscv-env
```

Start your container for the first time with:
```bash
docker run -it -v <optional directory>:/project --name rvenv rhitdeca/riscv-env:latest bash
```
* `-it` - creates an interactive terminal for you to type commands into.
* `--name rvenv` - names this container `rvenv`.
* `-v <optional directory>:/project` - mounts `<optional directory>` on your host computer to `/project` in this container. You do not need to provide this option if you don't want a shared folder between this container and your host machine.

## Running subsequent times
See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building
To build this image, run the following command:
```bash
# cd into this folder first
# Make sure to replace <version> with your version number for the image you're building
docker build . -t rhitdeca/riscv-env:<version>
```