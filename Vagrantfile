# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  # HGFS kernel module currently doesn't load correctly for native shares.
  config.vm.synced_folder ".", "/vagrant", type: 'nfs'

  # Ubuntu 14.04 - Trusty Tahr
  config.vm.define "ubuntu1404" do |ubuntu1404|
    ubuntu1404.vm.hostname = "ubuntu1404test"
    ubuntu1404.vm.box = "geerlingguy/ubuntu1404"
    ubuntu1404.vm.network :private_network, ip: "192.168.3.2"

    # VirtualBox.
    ubuntu1404.vm.provider :virtualbox do |v|
      v.name = "ubuntu1404.dev"
      v.memory = 1024
      v.cpus = 3
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    # Ansible.
    ubuntu1404.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.sudo = true
    end
  end

  # Ubuntu 12.02 - Precise Pangolin
  config.vm.define "ubuntu1204" do |ubuntu1204|
    ubuntu1204.vm.hostname = "ubuntu1204test"
    ubuntu1204.vm.box = "geerlingguy/ubuntu1204"
    ubuntu1204.vm.network :private_network, ip: "192.168.3.3"

    # VirtualBox.
    ubuntu1204.vm.provider :virtualbox do |v|
      v.name = "ubuntu1204.dev"
      v.memory = 1024
      v.cpus = 3
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    # Ansible.
    ubuntu1204.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.sudo = true
    end
  end

  # CentOS 7
  config.vm.define "centos7" do |centos7|
    centos7.vm.hostname = "centos7test"
    centos7.vm.box = "geerlingguy/centos7"
    centos7.vm.network :private_network, ip: "192.168.3.4"

    # VirtualBox.
    centos7.vm.provider :virtualbox do |v|
      v.name = "centos7.dev"
      v.memory = 1024
      v.cpus = 3
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    # Ansible.
    centos7.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.sudo = true
    end
  end

  # CentOS 6
  config.vm.define "centos6" do |centos6|
    centos6.vm.hostname = "centos6test"
    centos6.vm.box = "geerlingguy/centos6"
    centos6.vm.network :private_network, ip: "192.168.3.5"

    # VirtualBox.
    centos6.vm.provider :virtualbox do |v|
      v.name = "centos6.dev"
      v.memory = 1024
      v.cpus = 3
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    # Ansible.
    centos6.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.sudo = true
    end
  end
end
