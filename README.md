# Kubernetes (K8s)

[![GoDoc Widget]][GoDoc] [![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/569/badge)](https://bestpractices.coreinfrastructure.org/projects/569)

<img src="https://github.com/kubernetes/kubernetes/raw/master/logo/logo.png" width="100">

----

Kubernetes, also known as K8s, is an open source system for managing [containerized applications]
across multiple hosts. It provides basic mechanisms for deployment, maintenance,
and scaling of applications.

Kubernetes builds upon a decade and a half of experience at Google running
production workloads at scale using a system called [Borg],
combined with best-of-breed ideas and practices from the community.

Kubernetes is hosted by the Cloud Native Computing Foundation ([CNCF]).
If your company wants to help shape the evolution of
technologies that are container-packaged, dynamically scheduled,
and microservices-oriented, consider joining the CNCF.
For details about who's involved and how Kubernetes plays a role,
read the CNCF [announcement].

----

## To start using K8s

See our documentation on [kubernetes.io].

```

free -h 
sudo -i
```

Disable swapoff
```
swapoff -a
free -h 
```


 Comment all line starting with swap :
```
vi /etc/fstab   
```

# Ubuntu OS Detais Check : -
```
cat /etc/os-release
```
# Install Docker using the repository🔗

 Uninstall old versions🔗
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```
 1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

 2.Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
3.Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
# INSTALL DOCKER ENGINE
  Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:
```
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io

 $ docker version
 ```
 Verify the MAC address and product_uuid are unique for every node :-
```
 $ sudo cat /sys/class/dmi/id/product_uuid
 ```
 
# Installing kubeadm, kubelet and kubectl :-

 You will install these packages on all of your machines:

  * kubeadm: the command to bootstrap the cluster.
  * kubelet: the component that runs on all of the machines in your cluster and does things like starting pods and containers.
  * kubectl: the command line util to talk to your cluster

  ```
  sudo apt-get update && sudo apt-get install -y apt-transport-https curl
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
  cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
  deb https://apt.kubernetes.io/ kubernetes-xenial main
  EOF
  sudo apt-get update
  sudo apt-get install -y kubelet kubeadm kubectl
  
  
 
  
 $ sudo apt-get update && sudo apt-get install -y apt-transport-https curl
   curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
   deb https://apt.kubernetes.io/ kubernetes-xenial main
   EOF

 $ sudo apt-get update
 $ sudo apt-get install -y kubelet kubeadm kubectl
```


 Configure Kubernetes Master : -

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

You can see from the output that there are several objects that are created here and to verify this installation please run the following:

```
 $ kubectl get nodes 
       
 $ kubectl get nodes -A
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:
```

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Alternatively, if you are the root user, you can run:
```

  export KUBECONFIG=/etc/kubernetes/admin.conf
```

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:
```

kubeadm join 10.0.2.12:6443 --token ed9xpd.o947vlq22kvwkrtf \
    --discovery-token-ca-cert-hash sha256:ab7494e9a79d11e02beaa1061b6cb39eed55b4caa0f5cb76d2b852278884bad5 
```


# Configure Kubernetes Network with Flannel

Flannel is an open-source virtual network project managed by CoreOS network designed for Kubernetes. Each host in a flannel cluster runs an agent called flanneld. It assigns each host a subnet, which acts as the IP address pool for containers running on the host. Containers can then contact other containers directly, using their IP address. Flannel supports multiple backends for encapsulating packets. The recommended choice is Virtual Extensible LAN (VXLAN), which runs a Layer 2 network on top of a Layer 3 infrastructure. Flannel also supports host-gw, which maps direct routes between hosts in a manner similar to Calico.


 https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/adding-windows-nodes/
 
 
 # What is a Pod?
 
 Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
 
 The shared context of a Pod is a set of Linux namespaces, cgroups, and potentially other facets of isolation - the same things that isolate a Docker container. Within a Pod's   context, the individual applications may have further sub-isolations applied.

 In terms of Docker concepts, a Pod is similar to a group of Docker containers with shared namespaces and shared filesystem volumes.
 
 Pods in a Kubernetes cluster are used in two main ways:
 
  * Pods that run a single container
  * Pods that run multiple containers that need to work together.
  
  # How Pods manage multiple containers :-
  
  For example, you might have a container that acts as a web server for files in a shared volume, and a separate "sidecar" container that updates those files from a remote       source, as in the following diagram:
  
  <img src="https://d33wubrfki0l68.cloudfront.net/aecab1f649bc640ebef1f05581bfcc91a48038c4/728d6/images/docs/pod.svg" width="500">
  
   Some Pods have init containers as well as app containers. Init containers run and complete before the app containers are started.

   Pods natively provide two kinds of shared resources for their constituent containers: networking and storage.





