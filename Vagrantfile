IMAGE_NAME = "peru/my_ubuntu-20.04-server-amd64"
IMAGE_VERSION = "20210222.01"
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
        config.vm.box_version = IMAGE_VERSION
        master.vm.network "public_network", ip: "10.149.69.69", bridge: "eno1"
        master.vm.hostname = "ceph-honeybee"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ceph-playbook.yml"
        end
    end
end