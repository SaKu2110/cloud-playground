Vagrant.configure(2) do |config|
	config.ssh.insert_key = false
	config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
	config.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/home/vagrant/.ssh/id_rsa"

  	config.vm.define "target" do |node|
    	node.vm.box = "ubuntu/bionic64"
        node.vm.hostname = "target"
        node.vm.network :private_network, ip: "192.0.2.101"
        node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2220

		node.vm.provision :itamae do |itamae|
			itamae.sudo = true
			itamae.shell = '/bin/sh'
			itamae.recipes = '../roles/master.rb'
			itamae.json = '../nodes/node.json'
		end
	end

	config.vm.define "target-node" do |node|
        node.vm.box = "ubuntu/bionic64"
        node.vm.hostname = "target-node"
        node.vm.network :private_network, ip: "192.0.2.201"
        node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2230

		node.vm.provision :itamae do |itamae|
			itamae.sudo = true
			itamae.shell = '/bin/sh'
			itamae.recipes = '../roles/master.rb'
			itamae.json = '../nodes/node.json'
		end
	end
end
