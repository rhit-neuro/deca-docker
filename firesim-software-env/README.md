# firesim-software-env

## Features
This is the environment that you will use to build linux with the `firesim-software` repository. The environment has all the dependencies for building RISC-V Linux with buildroot.

## Running for the first time
Download this docker image with:
```bash
docker pull docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/firesim-software-env
```

Start your container for the first time with:
```bash
# <firesim-software repo location> is where you cloned the firesim-software repo
docker run -it -v <firesim-software repo location>:/project --name fsenv docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/firesim-software-env:latest bash
```
* `-it` - creates an interactive terminal for you to type commands into.
* `--name fsenv` - names this container `fsenv`.
* `-v <firesim-software repo location>:/project` - mounts `<firesim-software repo location>` on your host computer to `/project` in this container.

## Running subsequent times
See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building
To build this image, run the following command:
```bash
# cd into this folder first
# Make sure to replace <version> with your version number for the image you're building
docker build . -t docker.csse.rose-hulman.edu/neuroprocessor-group/deca-docker/firesim-software-env:<version>
```