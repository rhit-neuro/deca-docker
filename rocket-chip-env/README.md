# rocket-chip-env

## Features
The `rocket-chip-env` docker image has `riscv-tools` and `Xilinx Vivado` installed and is ready to build a `rocket-chip` from scratch targeting either the `verilator` or an actual FPGA. This image can also compile and run `Chisel` code.

## Running for the first time
**Note**: This image is large (~8GB compressed, ~20GB extracted). It will take a while to download.

Download this docker image with:
```bash
docker pull rhitdeca/rocket-chip-env
```
If there are any problems with this docker image, download this docker image instead. It is known to work:
```bash
docker pull rhitdeca/rocket-chip-env:1.1.1
```
Now `cd` into the directory with the Rocket Chip project you're working on (probably `deca/`). For example, if you're using the [`deca`](https://github.com/rhit-neuro/deca) repository as the base for your project, `cd` into the `deca` directory. Now, to create a new docker container from this docker image, run:
```bash
docker run -it --name rcenv -v $(pwd):/project -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY rhitdeca/rocket-chip-env
```
* `-it` - creates an interactive terminal for you to type commands into.
* `--name rcenv` - names this container `rcenv`.
* `-v $(pwd):/project` - mounts your current directory to `/project` in this container. You could alternatively replace `$(pwd)` with the absolute path on your host computer to whatever folder you want to mount at `/project` in this container.
* `-v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY` - handles connecting programs like `Vivado` running in this container to your display outside the container.

## Running subsequent times
See [`README.md`](../README.md#running-containers-subsequent-times) in this directory's parent directory.

## Building
You probably won't need to rebuild this image from scratch as you can just download a prebuilt image from this repo's docker registry. If you do rebuild this image, you'll need around 75 GB of free space on your computer.

> **_Tip:_** If you don't have much room on your main drive, you can temporarily configure docker to run on an external drive to build this image. The following assumes your external drive is mounted at `/mnt/my-drive`:
>
> 1. `sudo systemctl stop docker`
> 2. `mkdir /mnt/my-drive/docker-base`
> 3. Create a `/etc/docker/daemon.json` file with the following contents:
>    ```
>    {
>        "graph": "/mnt/my-drive/docker-base"
>    }
>    ```
> 4. `sudo systemctl start docker`
> 5. Build and push your docker image to dockerhub
> 6. `sudo systemctl stop docker`
> 7. `sudo rm /etc/docker/daemon.json`
> 8. `sudo systemctl start docker`
> 9. Pull your image from dockerhub

First, you'll need to download [Vivado 2016.2](https://www.xilinx.com/member/forms/download/xef.html?filename=Xilinx_Vivado_SDK_2016.2_0605_1.tar.gz). This download requires you to create an account with Xilinx. Place the downloaded file (named `Xilinx_Vivado_SDK_2016.2_0605_1.tar.gz`) in this directory and then run the following:
```bash
# Make sure to replace <version> with your version number for the image you're building
docker build . -t rhitdeca/rocket-chip-env:<version>
```
Note: this build will take some time and a large amount of disk space

### `install_config.txt`
`install_config.txt` is a configuration file required for installing `Vivado`. A `install_config.txt` file is already included in this directory, so you don't need to make a new one. Details of these config files and how to generate them can be found here: https://www.xilinx.com/html_docs/xilinx2018_2/sdsoc_doc/generating-configuration-file-toz1504034318049.html
