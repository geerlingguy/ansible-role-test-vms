# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Set to 'true' when testing new base box builds locally.
TEST_MODE = false
# LOCAL_BOX_DIRECTORY = "file://~/Downloads/"

# Uncomment when explicitly testing VirtualBox.
PROVIDER_UNDER_TEST = "virtualbox"
NETWORK_PRIVATE_IP_PREFIX = "172.16.3."

# Uncomment when explicitly testing VMWare.
# PROVIDER_UNDER_TEST = "vmware"
# NETWORK_PRIVATE_IP_PREFIX = "192.168.3."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', type: 'nfs'

  # VMware Fusion.
  config.vm.provider :vmware_fusion do |v, override|
    v.gui = false
    v.vmx["memsize"] = 1024
    v.vmx["numvcpus"] = 1
  end

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.gui = false
    v.memory = 1024
    v.cpus = 1
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Ubuntu 16.04 - Xenial Xerus
  config.vm.define "ubuntu1604" do |ubuntu1604|
    ubuntu1604.vm.hostname = "ubuntu1604test"
    if not TEST_MODE
      ubuntu1604.vm.box = "geerlingguy/ubuntu1604"
    else
      ubuntu1604.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-ubuntu1604.box"
    end
    ubuntu1604.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "2"

    # Ansible.
    ubuntu1604.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # Ubuntu 14.04 - Trusty Tahr
  config.vm.define "ubuntu1404" do |ubuntu1404|
    ubuntu1404.vm.hostname = "ubuntu1404test"
    if not TEST_MODE
      ubuntu1404.vm.box = "geerlingguy/ubuntu1404"
    else
      ubuntu1404.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-ubuntu1404.box"
    end
    ubuntu1404.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "3"

    # Ansible.
    ubuntu1404.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # Ubuntu 12.04 - Precise Pangolin
  config.vm.define "ubuntu1204" do |ubuntu1204|
    ubuntu1204.vm.hostname = "ubuntu1204test"
    if not TEST_MODE
      ubuntu1204.vm.box = "geerlingguy/ubuntu1204"
    else
      ubuntu1204.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-ubuntu1204.box"
    end
    ubuntu1204.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "4"

    # Ansible.
    ubuntu1204.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # CentOS 7
  config.vm.define "centos7" do |centos7|
    centos7.vm.hostname = "centos7test"
    if not TEST_MODE
      centos7.vm.box = "geerlingguy/centos7"
    else
      centos7.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-centos7.box"
    end
    centos7.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "5"

    # Ansible.
    centos7.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # CentOS 6
  config.vm.define "centos6" do |centos6|
    centos6.vm.hostname = "centos6test"
    if not TEST_MODE
      centos6.vm.box = "geerlingguy/centos6"
    else
      centos6.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-centos6.box"
    end
    centos6.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "6"

    # Ansible.
    centos6.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end
