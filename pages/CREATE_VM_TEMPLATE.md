# CREATE VM TEMPLATE

In order to provision proxmox vms using terraform and cloudinit vm templates are needed, here a quick reference of the steps to follow

- download server image of the needed operating system

- copy to the server scp `<file> <proxmox host>:/tmp`

- copy to the iso folder `cp /tmp/<file> /var/lib/vz/templates/iso`

- install os inside the machine and insert the ssh key

- convert the vm into template from UI

## ARCH VM TEMPLATE

refer to this [guide](https://wiki.archlinux.org/title/Arch_Linux_on_a_VPS#Proxmox)
