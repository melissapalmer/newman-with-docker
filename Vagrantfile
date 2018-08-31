Vagrant.configure("2") do |config|

#https://blog.zencoffee.org/2016/08/ansible-vagrant-windows/
  
  config.vm.box = "ubuntu/xenial64"
  
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
 
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.cpus = "1"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    
     vb.name = "newman-docker-vm"
  end
  
  # Configure the hostname for the default machine
  config.vm.define "newman-docker-vm" 
    
  config.vm.network "forwarded_port", 
	guest: 4751, host: 4751
	
  config.vm.network "public_network", bridge: "Realtek PCIe GBE Family Controller"	
  config.vm.network "public_network", bridge: "Intel(R) Dual Band Wireless-AC 7265"

  # Mount this folder as RO in the guest, since it contains secure stuff
  config.vm.synced_folder "playbooks", "/playbooks", :mount_options => ["ro"]  

  config.vm.provision 'ansible1', run: 'always', type: :ansible_local do |ansible1|
    ansible1.compatibility_mode = "2.0"
    ansible1.galaxy_role_file = 'playbooks/requirements.yml'
    ansible1.playbook = "playbooks/init.yml"
  end 

  config.vm.provision 'ansible2', run: 'always', type: :ansible_local do |ansible2|
    ansible2.compatibility_mode = "2.0"
    ansible2.playbook = "playbooks/common.yml"
    ansible_ssh_common_args='-o StrictHostKeyChecking=no'
  end 
  
  config.vm.provision 'ansible3', run: 'always', type: :ansible_local do |ansible3|
    ansible3.compatibility_mode = "2.0"
    ansible3.playbook = "playbooks/docker.yml"
    ansible_ssh_common_args='-o StrictHostKeyChecking=no'
  end 
end