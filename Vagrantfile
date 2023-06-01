# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
:inetRouter => {
        :box_name => "generic/debian11",
        :net => [
                   {auto_config: false, adapter: 2, virtualbox__intnet: "rI-rO1"},
                   {auto_config: false, adapter: 3, virtualbox__intnet: "rI-rO2"}
                ],
	:config => "router.yml"
  },
  :officeRouter => {
        :box_name => "generic/debian11",
        :net => [
                   {auto_config: false, adapter: 2, virtualbox__intnet: "rI-rO1"},
                   {auto_config: false, adapter: 3, virtualbox__intnet: "rI-rO2"},
                   {auto_config: false, adapter: 4, virtualbox__intnet: "lan"}
                ],
	:config => "router.yml"
  },
  :server1 => {
        :box_name => "generic/debian11",
        :net => [
                   {auto_config: false, adapter: 2, virtualbox__intnet: "lan"}
                ],
	:config => "pc.yml"
  },
  :client1 => {
        :box_name => "generic/debian11",
        :net => [
                   {auto_config: false, adapter: 2, virtualbox__intnet: "lan"}
                ],
	:config => "pc.yml"
  }
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s
	
	box.vm.provider "virtualbox" do |v|
        	# Set VM RAM size and CPU count
        	v.memory = "1024"
        	v.cpus = "1"
     	 end

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end

	if boxconfig[:config].length > 0
#	if MACHINES.keys.last == boxname
      		box.vm.provision "ansible" do |ansible|
	          ansible.playbook = "ansible/" + boxconfig[:config]
       		  ansible.verbose = "v"
#		  if boxname.to_s.include? "Server"
#		    	  ansible.extra_vars = { work_ip: boxconfig[:net][0][:ip]}
#		  end
		end
	end
      end
  end
end

