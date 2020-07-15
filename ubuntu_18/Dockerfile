FROM ubuntu:16.04
LABEL maintainer="Emiliano Borghi"

ARG uid
ENV USER docker_ros

# Setup environment
RUN apt-get update && apt-get install -y locales software-properties-common
RUN locale-gen en_US.UTF-8
ENV \
  LANG=en_US.UTF-8 \
  DEBIAN_FRONTEND=noninteractive \
  TERM=xterm

# Tmux
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    git \
    sudo \
    tmux

# Create a user with passwordless sudo
RUN adduser --gecos "Development User" --disabled-password -u ${uid} $USER
RUN adduser $USER sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER root

# nvidia-docker2 for Ubuntu18.04
# FROM nvidia/opengl:1.0-glvnd-runtime-ubuntu18.04 as nvidia
# RUN rm -rf /var/lib/apt/lists/*
# ENV NVIDIA_VISIBLE_DEVICES=all 
# ENV NVIDIA_DRIVER_CAPABILITIES=all

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils


COPY 10_nvidia.json /usr/share/glvnd/egl_vendor.d/10_nvidia.json

USER $USER
CMD tmux