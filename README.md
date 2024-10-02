# Kubernetes Installation on Ubuntu 22.04

## For Linux OS

### Install VirtualBox, Vagrant and Git

Install Virtualbox, Vagrant and Git on the laptop or PC

> [Virtualbox](https://www.virtualbox.org/)

> [Vagrant](https://www.vagrantup.com/)

> [GIT](https://git-scm.com/)

Install the necessary plugins

```bash
vagrant plugin install vagrant-hostmanager
```

## For Windows 10/11 OS

### Install VMware Workstation(VMware destop plugin) or VirtualBox, Vagrant and Git

> [VMWare Workstation](https://www.vmware.com/products/workstation-pro.html)

> [VMWare Desktop Plugin](https://developer.hashicorp.com/vagrant/docs/providers/vmware/vagrant-vmware-utility)

OR

> [Virtualbox](https://www.virtualbox.org/)

> [Vagrant](https://www.vagrantup.com/)

> [GIT](https://git-scm.com/)

Install the required plugins for vmwaredesktop

```bash
vagrant plugin install vagrant-vmware-desktop
vagrant plugin install vagrant-hostmanager
```

Install the required plugins for virtualbox

```bash
vagrant plugin install vagrant-hostmanager

```

### Clone the repository

Clone the repo to the desired location

```bash
git clone https://github.com/mialeevs/Kubernetes_installation_vagrant.git
cd kubernetes_installation_vagrant

# Rename the Vagrant file based on the provider to "Vagrantfile" and run below command
vagrant up
```

## On the Kube master server

Initialize the cluster by passing the cidr value and the value will depend on the type of network CLI you choose.

Note: Disable swap on all the nodes before running the init command

```bash
sudo swapoff -a

# comment the swap entry
sudo vim /etc/fstab
```

```bash
# For Virtual Box
sudo kubeadm init --apiserver-advertise-address=192.168.56.10 --pod-network-cidr=10.244.0.0/16

# For VMWare Desktop
sudo kubeadm init --apiserver-advertise-address=192.168.52.10 --pod-network-cidr=10.244.0.0/16

# Sample join command(You will get a kubeadm join command as shown below, save is safe)
# Run the kudeadm join command on both the worker nodes
sudo kubeadm join 192.168.52.10:6443 --token g8v4ma.r7z7xxxxxx1dnwb1 --discovery-token-ca-cert-hash sha256:930f85997fdfxxxxxxxxxxxxxxx8fd084f30a8b12080f3e4b530
```

### Start using the cluster with current user

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### To set up the Calico network

```bash
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.28.2/manifests/tigera-operator.yaml

curl https://raw.githubusercontent.com/projectcalico/calico/v3.28.2/manifests/custom-resources.yaml -O

# Update the ip value to 10.244.0.0/16
# vim custom-resources.yaml

kubectl create -f custom-resources.yaml

```

### To install metrics server

```bash
git clone https://github.com/mialeevs/kubernetes_installation_crio.git
cd kubernetes_installation_crio/
kubectl apply -f metrics-server.yaml
cd
rm -rf kubernetes_installation_crio/
```
