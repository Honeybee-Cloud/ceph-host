This repo contains code for deploying a HNYB Node VM on libvirt or virtualbox. 

## USAGE

You will need a Linux system with either libvirt or virtualbox and Vagrant installed along with some other utilities.

On VM Host:

Copy/Append the interfaces or 02-hnyb-libvirt-vm.yaml files depending on your distro.

On Ubuntu do:
`sudo cp 02-hnyb-libvirt-vm.yaml /etc/netplan/`
`sudo netplan generate`
`sudo netplan apply`

`git clone https://github.com/Honeybee-Cloud/hnyb-host`
`cd hnyb-host`
`vagrant up`

It will take time to provision the VM and run the Ansible config.

Currently (02-Mar-2021) the produced VM will need to be joined to the cluster manually. This is because the method through which node will join clusters is not yet designed.