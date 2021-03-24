# Dockerfile for tag rhitdeca/cuda-neuro-simulation-env:1.1.0
FROM rhitdeca/neuro-simulation-env:3.0.1

USER root

# Unzip/copy libwb source
ADD libwb.tar.gz /libwb/

# Install CUDA dependencies
RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  build-essential \
  wget \
  software-properties-common

# Get keys for CUDA 10.2
RUN \
  wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin && \
  mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600 && \
  wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb && \
  dpkg -i cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb && \
  apt-key add /var/cuda-repo-10-2-local-10.2.89-440.33.01/7fa2af80.pub && \
  rm cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb

# Install CUDA 10.2
RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install cuda && \
  apt-get autoremove

# Install CUDA 10.2 patches
RUN \
  wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/patches/1/cuda-repo-ubuntu1804-10-2-local_10.2.1-1_amd64.deb && \
  wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/patches/2/cuda-repo-ubuntu1804-10-2-local_10.2.2-1_amd64.deb && \
  dpkg -i cuda-repo-ubuntu1804-10-2-local_10.2.1-1_amd64.deb && \
  dpkg -i cuda-repo-ubuntu1804-10-2-local_10.2.2-1_amd64.deb && \
  rm cuda-repo-ubuntu1804-10-2-local_10.2.*.deb

# Build libwb
RUN \
  mkdir -p /libwb/build && \
  cd /libwb/build/ && \
  cmake .. && \
  make -j && \
  mv libwb.* ../ && \
  cd - && \
  rm -rf /libwb/build/

# Source CUDA's settings in rose user's bashrc
RUN \
  echo "export PATH=/usr/local/cuda-10.2/bin${PATH:+:${PATH}}" >> /home/rose/.bashrc && \
  echo "export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}" >> /home/rose/.bashrc && \
  echo "complete -W \"\\\`grep -oE '^[a-zA-Z0-9_.-]+:([^=]|$)' ?akefile | sed 's/[^a-zA-Z0-9_.-]*$//'\\\`\" make" >> /home/rose/.bashrc && \
  echo "PS1=\"\\[\\e]0;\\u@\\h: \\w\\a\\]${debian_chroot:+($debian_chroot)}\\[\\033[01;32m\\]\\u@\\h\\[\\033[00m\\]:\\[\\033[01;34m\\]\\w\\[\\033[00m\\]\\$ \"" >> /home/rose/.bashrc && \
  echo "\$include /etc/inputrc" > /home/rose/.inputrc && \
  echo "\"\\e[1;5A\": history-search-backward" >> /home/rose/.inputrc && \
  echo "\"\\e[1;5B\": history-search-forward" >> /home/rose/.inputrc && \
  touch /home/rose/.sudo_as_admin_successful

# Update Boost to 1.65.1 for CUDA
RUN rm -rf /usr/local/include/boost/*
ADD boost_1_65_1.tar.gz /usr/local/include/boost/

VOLUME /project
WORKDIR /project

USER rose

CMD bash
