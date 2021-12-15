# minecraft-server
The Asterion Pi Minecraft Server uses a Raspberry Pi 4 to run a Minecraft server using Lite Kubernetes (K3S) and Helm Chart deployments. This repository controls the code necessary to quickly deploying and maintaining this infrastructure.

# Contents
- [Pre-requisites](#prereqs)
- [Step 1 - Configure SSH Connectivity](#step1)
- [Step 2 - Install Lightweight Kubernetes (K3S)](#step2)
- [Step 3 - Install Helm and Deploy Minecraft Chart](#step3)

<hr>


## Prerequisites <a name='prereqs'></a>

1. I'm using a Windows 10 laptop with Windows Subsystem for Linux v2 (WSL2) installed. Please note that these instructions will represent this environment, accordingly.

2. Purchase a SD card with at least 8Gb of capacity. Recommend overkilling this with a 32Gb card, for future-proofing.

    - Ensure you have the means to flash this SD card. I'm using a USB adaptor for SD cards, so that I can plug it into my laptop and configure it in a familiar environment.

3. Download the latest Linux-based ARM64 operating system image from the [Official Raspberry Pi website](https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-11-08/).

>**Note:** We want to use a 64-bit operating system so that the Raspberry Pi 4 (RPI4) computer resources can be more effectively utilized. While the latest ARM64 images are still in Beta release, the images work very well for our purpose. 

4. Download the Raspberry Pi Imager from the [Official Raspberry Pi website](https://www.raspberrypi.com/software/), and install this on an accessible PC. We will use the imager to write the ARM64 operating system image to our SD card.

5. Insert the SD card into your PC, and use the Raspberry Pi Imager to write the image to the SD card.

>**Note:** A good site that references how to do this can be found [here](https://qengineering.eu/install-raspberry-64-os.html)

6. Insert the SD card into your RPI, and boot it up!

>**Note:** During the boot sequence, you may receive a number of prompts that require input to confirm the operating system configurations you want, such as timezone, keyboard layouts, location services, etc. Please make note of the root username and password.

<hr>


## Step 1 - Configure SSH Connectivity<a name='step1'></a>

Enabling SSH connectivity will allow us to remotely administer the Raspberry Pi, as well as provide an extra layer of security (aside from turning off SSH). 

1. Create SSH key pair in WSL2.

```ssh-keygen -t rsa -b 4096 -f ~/.ssh/minecraft-server -C "Minecraft Server key"```

2. Start the SSH agent on the client PC and add the identity to the key ring.

```eval $(ssh-agent -s) && ssh-add ~/.ssh/minecraft-server```

3. Once the Raspberry Pi has booted up, check that the SSH service is running.

```sudo systemctl status sshd```

4. If the SSH service isn't running, you will need to start it.

    - Open the Raspberry Pi configuration manager.
    ```sudo raspi-config```

    - Select *Interface Options* and enable the SSH service.

5. Obtain the local IP address from the Raspberry Pi.

```ifconfig```

6. Copy the newly-created public key hash to the Raspberry Pi authorised keys config file.

```ssh-copy-id -i ~/.ssh/minecraft-server.pub pi@<RPI4 node IP Address>```

>**Note:** Initial host key verification may fail if you've connected to this host before, and the server has a static local IP. We will need to remove the host key entry in our *known_hosts* file with ```ssh-keygen -f "/path/to/known_hosts/file" -R "<RPI4 node IP address>"```. 

7. Test the SSH connection.

```ssh pi@<RPI4 node IP address>```

Enter *Yes* at the prompt to re-add the new host key into your *known_hosts* file. You may be prompted for the user password you configured during the O/S install on the RPI4.

<hr>


## Step 2 - Install Lightweight Kubernetes (K3S) and Kubectl<a name='step2'></a>

We will install 

1. Connect to the Raspberry PI server through SSH.

```ssh pi@<RPI4 node IP address>```

2. Install K3S on both your server and working station/PC.

```curl -sfL https://get.k3s.io | sh -```

3. Install Kubectl on the server.

```curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl```

4. We'll need to configure K3S to be able to talk to our cluster. Because we're using a slim version of Kubernetes, we'll need to copy the default K3S configuration file (Kubeconfig) on our working station, to the default Kubernetes configuration path on the server.

```sudo scp /etc/rancher/k3s/k3s.yaml <YOUR_ACCOUNT>@<YOUR_WORKSTATION>:.kube/config```

>**Note:** You will need to edit the file under *~/.kube/config* and replace the current server IP address (127.0.0.1) with the actual local IP address.

5. Create a Minecraft Namespace and Context

To isolate users and pods to a specific entity, we can create a namespace and context, and switch between contexts as required.

```
kubectl create namespace minecraft
kubectl config set-context minecraft --namespace=minecraft --user=default --cluster=default
kubectl config use-context minecraft
```

<hr>


## Step 3 - Install Helm and Deploy Minecraft Chart<a name='step3'></a>

Testing Testing
