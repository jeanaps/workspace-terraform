# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"

##Criando VM Terraform
  config.vm.define "terraform" do |terraform|
  config.vm.box = "ubuntu/bionic64"
    terraform.vm.hostname = "terraform"
    terraform.vm.network :private_network, ip: "192.168.38.240"
    terraform.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=750,fmode=600"]
    terraform.vm.provider :virtualbox do |v|
      v.name = "terraform"
      v.memory = 512
      v.cpus = 1
    end
  end
  
  ##Criando VM Proxmox
  config.vm.define "proxmox" do |proxmox|
    proxmox.vm.hostname = "proxmox"
    proxmox.vm.network :private_network, ip: "192.168.38.245"
    proxmox.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=750,fmode=600"]
    proxmox.vm.provider :virtualbox do |v|
      v.name = "proxmox"
      v.memory = 512
      v.cpus = 1
    end
  end

  ##Criando VM Controller Ansible
  config.vm.define "controller" do |controller|
    controller.vm.hostname = "controller"
    controller.vm.network :private_network, ip: "192.168.38.241"
    controller.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=750,fmode=600"]
    controller.vm.provider :virtualbox do |v|
      v.name = "AnsibleController"
      v.memory = 512
      v.cpus = 1
    end

    ## Integrando o Ansible no Provisionamento
    controller.vm.provision :ansible_local do |ansible|
      ansible.install_mode = "default"
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "inventory"
      ansible.verbose  = true
      ansible.install  = true
      ansible.limit    = "all"
    end
  end

end
#

