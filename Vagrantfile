# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

require 'yaml'

dir = File.dirname(File.expand_path(__FILE__))

configValues = YAML.load_file("#{dir}/config.yml")
project     = configValues['magentocloud']
vmdata         = configValues['vagrantfile']

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "debian/jessie64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false
  
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  config.vm.provider :virtualbox do |v|
    v.name = "#{project['project_name']}" + "." + "#{vmdata['vm']['hostname_base']}"
    v.memory = "#{vmdata['vm']['memory']}"
    v.cpus = "#{vmdata['vm']['cpus']}"
    # Share VPN connections
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # Use multiple CPUs in VM
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  
  # analytics server internal API
  config.vm.network "forwarded_port", guest: 8081, host: 8081, protocol: 'tcp'
  
  # webpack nodejs dev server
  config.vm.network "forwarded_port", guest: 8082, host: 8082
  
  # mongodb to connect from host
  # config.vm.network "forwarded_port", guest: 27017, host: 27117

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.insert_key = false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  
  config.vm.hostname = "#{project['project_name']}" + "." + "#{vmdata['vm']['hostname_base']}"
  config.vm.network :private_network, ip: "#{vmdata['vm']['network']['private_network']}"
  
  config.vm.define :magentocloud do |magentocloud|
  end
  
  # We disable the synced folder on first boot, so we can put the platform project in the proper folder, and then share it.
  config.vm.synced_folder "app", "/app", id: "app", type: "nfs"

  # Magento repo Git keys
  config.vm.provision "file", source: "#{project['project_ssh_key']}", destination: "~/.ssh/id_rsa"
  config.vm.provision "file", source: "#{project['project_ssh_key_pub']}", destination: "~/.ssh/id_rsa.pub"

  # Ansible provisioning.
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.sudo = true
  end

  #config.vm.provision "shell",
  #  path: "provisioning/ansible.sh"

  #config.vm.provision "shell",
  #  inline: "sudo ansible-galaxy install -f -r /vagrant/provisioning/requirements  > /dev/null 2>&1",
  #  keep_color: true

    # Ansible provisioner.
  #config.vm.provision "shell",
  #  inline: "PYTHONUNBUFFERED=1 ANSIBLE_FORCE_COLOR=true ansible-playbook /vagrant/provisioning/playbook.yml -i /vagrant/provisioning/inventory --connection=local --sudo --extra-vars 'project_name=#{project['project_name']} hostname_base=#{vmdata['vm']['hostname_base']}'",
  #  keep_color: true


end
