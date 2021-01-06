# Kubernetes-Setup
Kubernetes is an open-source container-orchestration system for automating computer application deployment, scaling, and management. It was originally designed by Google and is now maintained by the Cloud Native Computing Foundation. 




free h 
---------------------------------
sudo -i
---------------------------------
swapoff -a
---------------------------------
swapo
---------------------------------
free -h 
---------------------------------
vi /etc/fstab   #comment all line starting with swap 

# Ubuntu OS Detais Check : -
cat /etc/os-release

# Install Docker using the repository🔗

# Uninstall old versions🔗

$ sudo apt-get remove docker docker-engine docker.io containerd runc

# 1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

$ sudo apt-get update
----------------------------------------------------------
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

# 2.Add Docker’s official GPG key:

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# 3.Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# INSTALL DOCKER ENGINE
  Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io

 $ docker version
 
# Verify the MAC address and product_uuid are unique for every node :-

 sudo cat /sys/class/dmi/id/product_uuid
 
 
# Installing kubeadm, kubelet and kubectl :-


sudo apt-get update && sudo apt-get install -y apt-transport-https curl

---------------------------------
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
---------------------------------
sudo apt-get update
---------------------------------
sudo apt-get install -y kubelet kubeadm kubectl
---------------------------------
# Configure Kubernetes Master : -

sudo kubeadm init --pod-network-cidr=10.244.0.0/16
---------------------------------
kubectl get nodes





 

