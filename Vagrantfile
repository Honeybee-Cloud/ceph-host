IMAGE_NAME = "bento/ubuntu-20.04"

N = 1

Vagrant.configure("2") do |config|

    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2

        file_to_disk = 'disk2.vdi'
        unless File.exist?(file_to_disk)
          # 50 GB
          v.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]
    end

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
