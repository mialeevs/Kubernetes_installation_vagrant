Vagrant.configure(2) do |config|

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true

  config.vm.define "k8s_cp" do |cp|
    cp.vm.box = "ubuntu/jammy64"
    # cp.vm.box = "bento/ubuntu-22.04"
    cp.vm.network "private_network", ip: "192.168.56.10"
    cp.vm.hostname = "cp"
    cp.vm.boot_timeout = 300
    cp.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end
    cp.vm.provision "shell", path: "scripts/install.sh"
  end

  config.vm.define "k8s_w1" do |w1|
    w1.vm.box = "ubuntu/jammy64"
    # w1.vm.box = "bento/ubuntu-22.04"
    w1.vm.network "private_network", ip: "192.168.56.21"
    w1.vm.hostname = "w1"
    w1.vm.boot_timeout = 300
    w1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    w1.vm.provision "shell", path: "scripts/install.sh"
  end

  config.vm.define "k8s_w2" do |w2|
    w2.vm.box = "ubuntu/jammy64"
    # w2.vm.box = "bento/ubuntu-22.04"
    w2.vm.network "private_network", ip: "192.168.56.22"
    w2.vm.hostname = "w2"
    w2.vm.boot_timeout = 300
    w2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    w2.vm.provision "shell", path: "scripts/install.sh"
  end
 end
end


