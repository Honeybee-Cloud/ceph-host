IMAGE_NAME = "debian/buster64"
N = 2

Vagrant.configure("2") do |config|
    config.vm.network "forwarded_port", guest: 22, host: 22
    config.ssh.insert_key = false

    config.vm.provider :libvirt do |libvirt|
        libvirt.memory = 8192
        libvirt.cpus = 4
    end
      
    config.vm.define "hnyb-host" do |node0|
        node0.vm.box = IMAGE_NAME
        node0.vm.network "public_network", :type => "bridge", ip: "10.149.69.70", bridge: "br0", dev: "br0", mode: "bridge"
        node0.vm.hostname = "honeybee-vm0"
        node0.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbook.yml"
        end
    end
end
