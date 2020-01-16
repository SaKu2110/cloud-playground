Vagrant.configure(2) do |config|
	config.ssh.insert_key = false
	config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
	config.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/home/vagrant/.ssh/id_rsa"

  	config.vm.define "target" do |node|
    	node.vm.box = "ubuntu/bionic64"
        node.vm.hostname = "master"
        node.vm.network :private_network, ip: "192.0.2.101"
		node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2220
	end

	config.vm.define 'target-node' do |node|
        node.vm.box = 'ubuntu/bionic64'
        node.vm.hostname = 'worker'
        node.vm.network :private_network, ip: '192.0.2.201'
		node.vm.network :forwarded_port, id: 'ssh', guest: 22, host: 2230

		node.vm.provision 'ansible' do |ansible|
			ansible.playbook = 'site.yml'
			ansible.inventory_path = 'development'
			ansible.limit = 'all'
		end
	end
end
