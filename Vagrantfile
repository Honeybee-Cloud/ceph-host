IMAGE_NAME = "debian/buster64"

N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
      
    (1..N).each do |i|
        config.vm.define "hnyb-host-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "public_network", :type => "bridge", bridge: "br0", dev: "br0", mode: "bridge"
            node.vm.hostname = "honeybee-vm#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "playbook.yml"
            end
        end
    end
end
