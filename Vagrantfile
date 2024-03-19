Vagrant.configure("2") do |config|
  # Provisioning shell script to update packages and set up hosts file
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      echo "10.0.0.10  master-node" >> /etc/hosts
      echo "10.0.0.11  worker-node01" >> /etc/hosts
      echo "10.0.0.12  worker-node02" >> /etc/hosts
  SHELL
  
  # Configuration for the master node
  config.vm.define "master" do |master|
    master.vm.box = "bento/ubuntu-22.04"  # Ubuntu 22.04 image
    master.vm.hostname = "master-node"     # Hostname for the master node
    master.vm.network "private_network", ip: "10.0.0.10"  # Private network IP address
    master.vm.provider "virtualbox" do |vb|
        vb.memory = 4048  # Memory allocation for the master node
        vb.cpus = 2       # CPU allocation for the master node
    end
  end

  # Configuration for worker nodes using loop
  (1..2).each do |i|
    config.vm.define "node0#{i}" do |node|
      node.vm.box = "bento/ubuntu-22.04"  # Ubuntu 22.04 image
      node.vm.hostname = "worker-node0#{i}"  # Hostname for each worker node
      node.vm.network "private_network", ip: "10.0.0.1#{i}"  # Private network IP address for each worker node
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048  # Memory allocation for each worker node
          vb.cpus = 1       # CPU allocation for each worker node
      end
    end
  end
end
