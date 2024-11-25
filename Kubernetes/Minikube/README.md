
# Minikube Start
## What you’ll need
* 2 CPUs or more
* 2GB of free memory
* 20GB of free disk space
* Internet connection
* Container or virtual machine manager, such as: **Docker, Hyper-V, KVM,**

# 1. Install Docker 
## Install using the apt repository.
### 1. Set up Docker's apt repository.
##### Add Docker's official GPG key:
#
    sudo apt-get update
#
    sudo apt-get install ca-certificates curl
# 
    sudo install -m 0755 -d /etc/apt/keyrings
# 
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
#
    sudo chmod a+r /etc/apt/keyrings/docker.asc

###### Add the repository to Apt sources:
#
    echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# 
    sudo apt-get update
# 
    sudo apt-get install docker.io -y
# 
    sudo apt install docker status
# 
    sudo chown $USER /var/run/docker.sock

# 2. Installation Kubectl 
### Before you begin
##### You must use a kubectl version that is within one minor version difference of your cluster. For example, a v1.30 client can communicate with v1.29, v1.30, and v1.31 control planes. Using the latest compatible version of kubectl helps avoid unforeseen issues.
### Install kubectl binary with curl on Linux
* Download the latest release with the command:
#
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"

* Validate the binary (optional)
# 
     curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl.sha256"
* Validate the kubectl binary against the checksum file:
#
    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
* If valid, the output is:
``
kubectl: OK
``
* Install kubectl
# 
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl'
* Test to ensure the version you installed is up-to-date:
#
    kubectl version --client
# 3. Installation
* Operating system: **Linux**
* Installer Type: **Debian Package**
#
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
#
    sudo dpkg -i minikube_latest_amd64.deb
# Start your Cluster
#
    minikube start
# Interact with your cluster
#
    kubectl get po -A
### OR
#
    minikube kubectl -- get po -A
# THANK YOU 