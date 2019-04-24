Dockerfiles
=========

There are currently three docker images we use:
* [rocket-chip-env](rocket-chip-env/)
* [neuro-simulation-env](neuro-simulation-env/)
* [firesim-software-env](firesim-software-env/)

Note: Each of these images has a default non-root user `rose` with password `Docker!`. The `rose` user is also in the `sudo` group.

## Setting up Docker
First, you'll want to install docker:
```bash
sudo apt install docker.io
```
Now you need to add your user to the `docker` group so that you don't need to be root to run docker commands:
```bash
sudo groupadd docker
# replace <username> with your computer username below
sudo usermod -aG docker <username>
```
Now logout of your computer and log back in for your group membership to be re-evaluated. Now you can start up the docker daemon with:
```bash
sudo systemctl start docker
```

Test your installation of Docker by running:
```bash
docker run hello-world
```

You don't need to stop Docker now, but you can with:
```bash
sudo systemctl stop docker
```
Don't restart your computer now, but in general after restarting your computer, you may need to start the docker daemon again.

### Make sure your docker's networking is working
Sometimes when installing docker on Ubuntu, you won't be able to properly resolve hostnames within a container. Perform the following to see if docker's networking is working for you:
```bash
docker pull ubuntu:artful
docker run -it --rm ubuntu:artful bash
getent hosts google.com
```
If the above `getent` command prints an IP address, then docker's networking is working properly for you. If instead you get an error, follow these steps and then perform the above test again:
* Edit `/etc/NetworkManager/NetworManager.conf` and comment out the line `dns=dnsmasq`
* `sudo service network-manager restart`
* `sudo service docker restart`

This solution was found at https://serverfault.com/a/791971.

## Using Docker
We recommend you complete at least the first part of the official [Get Started](https://docs.docker.com/get-started/) tutorial to familiarize yourself with docker.

### Download images
To download a docker image:
```bash
# replace <image name> with the name of the image you want to download
# e.g. rocket-chip-env
docker pull rhitdeca/<image name>:latest
```

### Running a container for the first time
See this directory's sub-directories for specific instructions for each image on running containers for the first time.

### Running containers subsequent times
Once you've created a container, you can start it with:
```bash
docker start <container name>
```
To start a shell in a running container, run:
```bash
docker exec -it <container name> bash
```
To stop a running container:
```bash
docker stop <container name>
```

### Managing your images and containers
#### Seeing your containers and images
If you want to see what images you have downloaded, run:
```bash
docker image ls
```
If you want to see which containers you have that are running, run:
```bash
docker container ls
```
If you want to see all your containers, run:
```docker
docker container ls -a
```
#### Deleting containers and images
If you want to delete a container, run:
```bash
# Replace <container name> with the name of the container to delete
docker rm <container name>
```
If you want to delete an image, you first have to delete all containers that use that image and then run:
```bash
# Replace <image name> with the name of the image to delete
docker image rm <image name>
```

## Making New Images
### Versioning
We use [Semantic Versioning/SemVer](https://semver.org/) scheme to bump the version of docker images. Version numbers look like `<major>.<minor>.<patch>`.
The rules of thumb to bump the version are:
  - If the new image only has new versions of secondary dependencies (dependencies except gcc, Boost, and Protobuf), bump patch
  - If the new image has new versions of primary dependencies (gcc, Boost, and Protobuf, their versions are hardcoded), bump the version according to their version change (if they bump major, we bump major, and so on)
  - If the new image adds or removes secondary dependencies (tools, utilities, etc.), bump minor
  - If the new image adds or removes primary dependencies (compile-time libraries), bump major

Make sure you update the version in the first line of `Dockerfile` and `.gitlab-ci.yml` too.
We use specific versions in `.gitlab-ci.yml` to prevent mistakes like forgetting to push the image which leads to inconsistent environment.

#### Versioning while developing a new image
While developing a new docker image, you should take a slightly different approach to version numbering. Let's look at an example to see a good way to handle versioning.

Let's say `neuro-simulation-env` is currently at version `2.3.1` and we want to add a new primary dependency which would bump our verision number to `3.0.0`. While you are experimenting with building this new image, start with version number `3.0.0_dev01`. If the changes you tried didn't actually work, then you just need to bump the dev number (`3.0.0_dev02`) for your next attept at building your new image. Once you get a dev image to work, you can change its version number to your target version number of `3.0.0`.

#### Tagging images
Tagging is the way you associate a version number with a docker image. You can change the version or tag of a docker image with the following:
```bash
docker tag <image name>:<original tag> <image name>:<new tag>
```

### Docker Registry Info
We have a docker registry hosted publicly on [Docker Hub](https://hub.docker.com/u/rhitdeca).

#### Registry login
If you want to update one of the docker images hosted in this repository's registry, you must first login:
```bash
# The username and password used here are for your Docker Hub account
docker login docker.io
```
note: you only need to login one time

### Upload images
After logging in, you can push built docker images to this repository's registry with the following:
```bash
docker push rhitdeca/<image name>:<image tag>
```

