Vagrant.configure(2) do |config|

  config.vm.define "k8s_master" do |master|
    master.vm.box = "ubuntu/jammy64"
    # master.vm.box = "bento/ubuntu-22.04"
    master.vm.network "private_network", ip: "192.168.56.10"
    master.vm.hostname = "master"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end
    master.vm.provision "shell", path: "scripts/install.sh"
  end

  config.vm.define "k8s_worker1" do |worker1|
    worker1.vm.box = "ubuntu/jammy64"
    # worker1.vm.box = "bento/ubuntu-22.04"
    worker1.vm.network "private_network", ip: "192.168.56.21"
    worker1.vm.hostname = "worker1"
    worker1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    worker1.vm.provision "shell", path: "scripts/install.sh"
  end

  config.vm.define "k8s_worker2" do |worker2|
    worker2.vm.box = "ubuntu/jammy64"
    # worker2.vm.box = "bento/ubuntu-22.04"
    worker2.vm.network "private_network", ip: "192.168.56.22"
    worker2.vm.hostname = "worker2"
    worker2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    worker2.vm.provision "shell", path: "scripts/install.sh"
  end
#  end
end


