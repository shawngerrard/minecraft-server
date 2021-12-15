# minecraft-server
The Asterion Pi Minecraft Server uses a Raspberry Pi 4 to run a Minecraft server using Lite Kubernetes (K3S) and Helm Chart deployments. This repository controls the code necessary to quickly deploying and maintaining this infrastructure.

# Contents
- [Pre-requisites](#prereqs)

<hr>

## Prerequisites <a name='prereqs'></a>

1. Install a Linux-based ARM64 operating system onto the Raspberry Pi 4 (RPI4). We use a 64-bit operating system so that the RPI4's computer resources can be more effectively utilized. As of 15 December 2021, a Buster ARM64 image is available, but is still in Beta release. You can find this image [here](https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-11-08/). We'll be using this image to host and administer our Minecraft server.

2. 