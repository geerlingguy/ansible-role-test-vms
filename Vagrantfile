VAGRANTFILE_API_VERSION = "2"

# Set to 'true' when testing new base box builds locally.
TEST_MODE = FALSE
LOCAL_BOX_DIRECTORY = "~/Downloads/"

# Uncomment when explicitly testing VirtualBox.
PROVIDER_UNDER_TEST = "virtualbox"
NETWORK_PRIVATE_IP_PREFIX = "10.30.148."

# Uncomment when explicitly testing VMWare.
# PROVIDER_UNDER_TEST = "vmware"
# NETWORK_PRIVATE_IP_PREFIX = "192.168.3."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 3
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # VMware Fusion.
  config.vm.provider :vmware_fusion do |v, override|
    v.vmx["memsize"] = 1024
    v.vmx["numvcpus"] = 3
  end

  # Ubuntu
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.hostname = "ubuntuTest"
    if not TEST_MODE
      ubuntu1604.vm.box = "ubuntu/trusty64"
    else
      ubuntu.vm.box = LOCAL_BOX_DIRECTORY + PROVIDER_UNDER_TEST + "-ubuntu.box"
    end
    ubuntu.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "2"

    # Ansible.
    ubuntu.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # CentOS 7
  config.vm.define "centos7" do |centos7|
    centos7.vm.hostname = "centos7test"
    if not TEST_MODE
      centos7.vm.box = "centos/7"
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
