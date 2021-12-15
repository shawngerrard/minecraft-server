# minecraft-server
The Asterion Pi Minecraft Server uses a Raspberry Pi 4 to run a Minecraft server using Lite Kubernetes (K3S) and Helm Chart deployments. This repository controls the code necessary to quickly deploying and maintaining this infrastructure.

# Contents
- [Pre-requisites](#prereqs)

<hr>

## Prerequisites <a name='prereqs'></a>

1. Purchase a SD card with at least 8Gb of capacity. 

    - Ensure you have the means to flash this SD card. I'm using a USB adaptor for SD cards, so that I can plug it into my laptop and configure it in a familiar environment.

2. Download the latest Linux-based ARM64 operating system image from the [Official Raspberry Pi website](https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-11-08/).

>**Note:** We want to use a 64-bit operating system so that the Raspberry Pi 4 (RPI4) computer resources can be more effectively utilized. While the latest ARM64 images are still in Beta release, the images work very well for our purpose. 

3. Download the Raspberry Pi Imager from the [Official Raspberry Pi website](https://www.raspberrypi.com/software/), and install this on an accessible PC. We will use the imager to write the ARM64 operating system image to our SD card.

4. Insert the SD card into your PC, and use the Raspberry Pi Imager to write the image to the SD card.

5. Insert the SD card into your RPI, and boot it up!

>**Note:** You may receive a number of prompts that require your input to confirm the configurations you want. Things like timezone, keyboard layouts, etc.

