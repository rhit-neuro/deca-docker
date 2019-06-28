# Template Dockerfile for creating application environments
FROM rhitdeca/riscv-env:1.0.0

# Install dependencies
RUN \
  apt-get update && \
  apt-get install -y \
  # put other dependencies here
  # each should be followed by a '\'
  # git \
  sudo && \
  rm -rf /var/lib/apt/lists/* && \
  # Create a "rose" user with password "Docker!"
  useradd -ms /bin/bash rose && \
  usermod -aG sudo rose && \
  echo "rose:Docker!" | chpasswd

# Build and install other dependencies you may need using RUN

VOLUME /project
WORKDIR /project

USER rose

CMD bash
