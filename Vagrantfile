# -*- mode: ruby -*-
# vi: set ft=ruby :

# Check required plugins
REQUIRED_PLUGINS = %w(vagrant-junos vagrant-host-shell vagrant-vyatta)
exit unless REQUIRED_PLUGINS.all? do |plugin|
  Vagrant.has_plugin?(plugin) || (
    puts "The #{plugin} plugin is required. Please install it with:"
    puts "$ vagrant plugin install #{plugin}"
    false
  )
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.


	config.vm.define "vsrx1" do |vsrx1|
	vsrx1.ssh.insert_key = false
	vsrx1.vm.network "private_network", virtualbox__intnet: "net1"
	vsrx1.vm.network "private_network", virtualbox__intnet: "net2"
	vsrx1.vm.network "private_network", virtualbox__intnet: "net3"
	vsrx1.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx1.vm.provider :virtualbox  do |vb|
		vb.name = "junos1"
		vb.memory = 1024
		end
	end


	config.vm.define "vsrx2" do |vsrx2|
	vsrx2.vm.network "private_network", virtualbox__intnet: "net1"
	vsrx2.vm.network "private_network", virtualbox__intnet: "net4"
	vsrx2.vm.network "private_network", virtualbox__intnet: "net5"
	vsrx2.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx2.vm.provider :virtualbox  do |vb|
		vb.name = "junos2"
		vb.memory = 1024
		end
	end


	config.vm.define "vsrx3" do |vsrx3|
	vsrx3.vm.network "private_network", virtualbox__intnet: "net2"
	vsrx3.vm.network "private_network", virtualbox__intnet: "net4"
	vsrx3.vm.network "private_network", virtualbox__intnet: "net5"
	vsrx3.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx3.vm.provider :virtualbox  do |vb|
		vb.name = "junos3"
		vb.memory = 1024
		end
	end


	config.vm.define "vsrx4" do |vsrx4|
	vsrx4.vm.network "private_network", virtualbox__intnet: "net3"
	vsrx4.vm.network "private_network", virtualbox__intnet: "net5"
	vsrx4.vm.network "private_network", virtualbox__intnet: "net6"
	vsrx4.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx4.vm.provider :virtualbox  do |vb|
		vb.name = "junos4"
		vb.memory = 1024
		end
	end

	config.vm.define "vsrx5" do |vsrx5|
	vsrx5.vm.network "private_network", virtualbox__intnet: "net5"
	vsrx5.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx5.vm.provider :virtualbox  do |vb|
		vb.name = "junos5"
		vb.memory = 512
		end
	end


	config.vm.define "vsrx6" do |vsrx6|
	vsrx6.vm.network "private_network", virtualbox__intnet: "net6"
	vsrx6.vm.box = "juniper/ffp-12.1X47-D15.4-packetmode"
	vsrx6.vm.provider :virtualbox  do |vb|
		vb.name = "junos6"
		vb.memory = 512
		end
	end


	if !Vagrant::Util::Platform.windows?
      config.vm.provision "ansible" do |ansible|
        ansible.groups = {
            "vsrx" => [
              "vsrx1",
              "vsrx2",
              "vsrx3",
              "vsrx4",
              "vsrx5",
              "vsrx6",
            ],
            "pe_vsrx" => [
              "vsrx3",
              "vsrx4"
            ],
            "ce_vsrx" => [
              "vsrx5",
              "vsrx6"
            ],
            "p_vsrx" => [
              "vsrx1",
              "vsrx2"
            ]
          }
          ansible.playbook = ansible.playbook = "vsrx.yml"
#         ansible.verbose = "vvv"
      end
  	end
end


