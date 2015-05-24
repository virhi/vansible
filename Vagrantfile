
Vagrant.require_version ">= 1.5"

Vagrant.configure("2") do |config|

    config.vm.provider :virtualbox do |v|
        v.name = "vansible"
        v.customize [
            "modifyvm", :id,
            "--name", "vansible",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end

    config.vm.box = "ubuntu/trusty64"
    
    config.vm.network :private_network, ip: "10.10.10.135"
    config.ssh.forward_agent = true

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
        ansible.extra_vars = {
            private_interface: "10.10.10.135",
            hostname: "vansible"
        }
    end
    
    config.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=777,fmode=777"]
end
