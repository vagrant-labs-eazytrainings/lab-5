# Variables pour la configuration
CPU = 2
RAM = "2048"
OS = "ubuntu/jammy64"

Vagrant.configure("2") do |config|
  # Configuration commune pour toutes les machines
  config.vm.provider "virtualbox" do |vb|
    vb.memory = RAM
    vb.cpus = CPU
  end

  # Machine 1 : Load Balancer (lb)
  config.vm.define "lb" do |lb|
    lb.vm.box = OS
    lb.vm.network "private_network", ip: "10.0.0.10"
  end

  # Machine 2 : Web Server 1 (web1)
  config.vm.define "web1" do |web1|
    web1.vm.box = OS
    web1.vm.network "private_network", ip: "10.0.0.11"

  end

  # Machine 3 : Web Server 2 (web2)
  config.vm.define "web2" do |web2|
    web2.vm.box = OS
    web2.vm.network "private_network", ip: "10.0.0.12"
  end
end
