# -*- mode: ruby -*-
# vi: set ft=ruby :

# 1. Define the dynamic nodes array first
nodes = [
  { name: "node-1", ip: "192.168.56.12" },
  { name: "node-2", ip: "192.168.56.13" }
]

Vagrant.configure("2") do |config|
  # Global setting for all machines
  config.vm.box = "ubuntu/focal64"

  # --- SECTION A: Static VMs ---
  
  # Web Server
  config.vm.define "web" do |web|
    web.vm.hostname = "web-server"
    web.vm.network "private_network", ip: "192.168.56.10"
    web.vm.provider "virtualbox" do |vb| 
      vb.memory = "1024" 
    end
  end

  # Database Server
  config.vm.define "db" do |db|
    db.vm.hostname = "db-server"
    db.vm.network "private_network", ip: "192.168.56.11"
    db.vm.provider "virtualbox" do |vb| 
      vb.memory = "2048" 
    end
  end

  # --- SECTION B: Dynamic Loop VMs ---
  
  nodes.each do |node_spec|
    config.vm.define node_spec[:name] do |node|
      node.vm.hostname = node_spec[:name]
      node.vm.network "private_network", ip: node_spec[:ip]
      
      # Optional: default hardware for the loop nodes
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
      end
    end
  end

end
