# falco-lab
This is a guide for installing Falco in Minikube on an Ubuntu EC2 instance.

## Step 1: Update system
Run the following commands to update all system packages to the latest release:

```
sudo apt update
sudo apt install apt-transport-https
sudo apt upgrade
```

If a reboot is required after the upgrade then perform the process.

```
[ -f /var/run/reboot-required ] && sudo reboot -f
```

## Step 2: Install KVM or VirtualBox Hypervisor
For VirtualBox users, install VirtualBox using:

```
sudo apt install virtualbox virtualbox-ext-pack
```

## Step 3: Download minikube on Ubuntu 22.04|20.04|18.04
You need to download the minikube binary. I will put the binary under /usr/local/bin directory since it is inside $PATH.

```
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```

Confirm version installed
```
minikube version
```

<img width="578" alt="Screenshot 2022-08-23 at 14 09 10" src="https://user-images.githubusercontent.com/109959738/186166290-974904d1-6b3c-423b-9f0f-c7a5be3bdefd.png">

## Step 4: Install kubectl on Ubuntu
We need kubectl which is a command line tool used to deploy and manage applications on Kubernetes:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

Make the kubectl binary executable.
```
chmod +x ./kubectl
```
Move the binary in to your PATH:
```
sudo mv ./kubectl /usr/local/bin/kubectl
```
Check version:
```
kubectl version -o json  --client
```

<img width="513" alt="Screenshot 2022-08-23 at 14 14 28" src="https://user-images.githubusercontent.com/109959738/186167355-22d4d249-81a0-4bff-937e-05e378a685ea.png">


## Installing Minikube

We need to bypass checks to avoid this issue:

<img width="1136" alt="Screenshot 2022-08-23 at 14 15 46" src="https://user-images.githubusercontent.com/109959738/186167695-53930dfb-6df6-4540-a8a0-6ce8028dceae.png">

The error message states that VT-X/AMD-V should be enabled in BIOS which is mandatory but this cannot be found in my BIOS settings.

```
minikube start --no-vtx-check
```

I tried the above command to resolve this issue and the minikube still had some issues.

<img width="1136" alt="Screenshot 2022-08-23 at 14 18 02" src="https://user-images.githubusercontent.com/109959738/186168228-80657c11-f3a0-497c-81ad-afaee4377589.png">
