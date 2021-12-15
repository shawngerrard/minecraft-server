# minecraft-server
The Asterion Pi Minecraft Server uses a Raspberry Pi 4 to run a Minecraft server using Lite Kubernetes (K3S) and Helm Chart deployments. This repository controls the code necessary to quickly deploying and maintaining this infrastructure.

# Contents
- [Pre-requisites](#prereqs)

<hr>

## Prerequisites <a name='prereqs'></a>

1. Flash a Linux-based ARM64 operating system image onto an SD card with at least 8Gb of RAM. 

>**Note:** We want to use a 64-bit operating system so that the Raspberry Pi 4 (RPI4) computer resources can be more effectively utilized.

As of 15 December 2021, a Bullseye ARM64 image is available, but is still in Beta release. You can find this image [here](https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-11-08/). We'll be using this image for our RPI4.

2. Insert the SD card into the RPI4 and boot it up! You may initially be asked some configuration questions before landing in the Operating System desktop for the administrative user.

