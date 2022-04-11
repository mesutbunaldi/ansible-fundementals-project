# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Box
  config.vm.box = "ubuntu/bionic64"
  
  config.vm.box_version = "20220325.0.0"

  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider & Specs
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 1
  end

  machines = %w[nginx rabbitmq redis kibana grafana vault]

  (2..7).each do |i|
		# Defining VM properties
		config.vm.define "#{machines[i-2]}" do |node|
			# Specifying the provider as VirtualBox and naming the VM's
			node.vm.hostname = "#{machines[i-2]}" 
      node.vm.network :private_network, ip: "192.168.56.#{i}"
		end
	end

 

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "install.yml"
    ansible.inventory_path = "inventory/dev/vagrant/hosts" 
    ansible.limit = "all"
    ansible.become = true
    ansible.verbose = "vv"
    #ansible.config+file = 'ansible.cfg'
  end

end
