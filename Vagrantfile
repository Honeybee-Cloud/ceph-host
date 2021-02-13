IMAGE_NAME = "bento/ubuntu-20.04"
N = 2

Vagrant.configure("2") do |config|
    config.vm.network "forwarded_port", guest: 22, host: 22
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
    end
      
    config.vm.define "ceph-host" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "public_network", ip: "10.149.69.69", bridge: "eno1"
        master.vm.hostname = "ceph-honeybee"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ceph-playbook.yml"
        end


        file_to_disk = 'disk2.vdi'
        unless File.exist?(file_to_disk)
          # 50 GB
          v.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATAController', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]
    
        file_to_disk = 'disk3.vdi'
        unless File.exist?(file_to_disk)
          # 50 GB
          v.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATAController', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]

        file_to_disk = 'disk4.vdi'
        unless File.exist?(file_to_disk)
          # 50 GB
          v.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATAController', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', file_to_disk]
    end
end