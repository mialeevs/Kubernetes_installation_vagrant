# Kubernetes Installation on Ubuntu 22.04

## For Linux OS

### Install Virtual box, Vagrant and Git

Install Virtualbox, Vagrant and Git on the laptop or PC

> [Virtualbox](https://www.virtualbox.org/)

> [Vagrant](https://www.vagrantup.com/)

> [GIT](https://git-scm.com/)

## For Windows 10/11 OS

### Installl VMware player/workstation, Vagrant, VMware destop plugin and Git

< [VMWare Workstation/Player](https://www.vmware.com/products/workstation-pro.html)

> [VMWare Desktop Plugin](https://developer.hashicorp.com/vagrant/docs/providers/vmware/vagrant-vmware-utility)

> [Vagrant](https://www.vagrantup.com/)

> [GIT](https://git-scm.com/)

### Clone the repo

Clone the repo to the desired location

```bash
git clone https://github.com/mialeevs/Kubernetes_installation_vagrant.git
cd kubernetes_installation_vagrant

# Rename the Vagrant file based on the provider to Vagrantfile and run below command
vagrant up
```

### On the Kube master server

Initialize the cluster by passing the cidr value and the value will depend on the type of network CLI you choose.

```bash
# For Virtual Box
sudo kubeadm init --apiserver-advertise-address=192.168.56.10 --pod-network-cidr=10.244.0.0/16

# For VMWare Desktop
sudo kubeadm init --apiserver-advertise-address=192.168.52.10 --pod-network-cidr=10.244.0.0/16
```

### Start using the cluster using current user

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### To set up the Calico network

```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### Install metrics server

```bash
git clone https://github.com/mialeevs/kubernetes_installation_crio.git
cd kubernetes_installation_crio/
kubectl apply -f metrics-server.yaml

```
