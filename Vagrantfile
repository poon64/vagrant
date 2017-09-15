# -*- mode: ruby -*-
# vi: set ft=ruby :

# Scania Proxy configuration
Vagrant.configure("2") do |config|
 if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://PROXYSESO.SCANIA.COM:8080"
    config.proxy.https    = "https://PROXYSESO.SCANIA.COM:8080"
    config.proxy.no_proxy = "localhost,127.0.0.1,.scania.com:8080"
  end

# OS
  config.vm.box = "bento/centos-7.3"

# Configure box with ansible provisioning
  config.vm.define "test" do |test|
    test.vm.hostname = "test"
    test.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "bootstrap.yml"
    end
    test.vm.network "private_network", ip: "192.168.33.31"
  end

  config.vm.define "docker" do |docker|
    docker.vm.hostname = "docker"
    docker.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "docker.yml"
    end
    docker.vm.network "private_network", ip: "192.168.33.11"
  end
end
