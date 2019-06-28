# application-env

## Features
The Dockerfile in this directory is just a template to make a development environment for your own application that will work with `deca`. The template extends the [`riscv-env`](../riscv-env) to make it easier to use the RISC-V toolchain.

## Building
To build this image, run the following command:
```bash
# cd into this folder first
# Make sure to replace <image name> and <version> with your image name and version number for the image you're building
docker build . -t <image name>:<version>
```