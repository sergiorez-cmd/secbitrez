# KVM Virt-manager Debian 12/13

## 1° Instalar pacotes

$ grep -E --color '(vmx|svm)' /proc/cpuinfo

$ sudo apt update

$ sudo apt install -y qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager

$ systemctl status libvirtd

$ sudo systemctl enable --now libvirtd

$ lsmod | grep -i kvm

## 2° Ativar rede virtual

$ sudo virsh net-start default

$ sudo virsh net-autostart default

$ sudo virsh net-list --all

## 3° Criar uma rede local bridge

$ sudo nano /etc/network/interfaces

### Primary network interface

auto enp2s0

iface enp2s0 inet manual

### Bridge definitions

auto br0

iface br0 inet static

bridge_ports enp2s0

bridge_stp off

address 192.168.1.254

network 192.168.1.0

netmask 255.255.255.0

broadcast 192.168.1.255

gateway 192.168.1.1

dns-nameservers 9.9.9.9 1.1.1.1

$ sudo systemctl restart networking.service

## Converter discos virtuais 

$ sudo apt install qemu-img

$ tar -xvf vm_disc.ova

$ qemu-img convert -p -f vmdk -O qcow2 vm_disc.vmdk new_vm_disc.qcow2

$ qemu-img convert -p -f vhdx -O qcow2 /virtual_disk_directory/vm_disk.vhdx /disk_directory/new_vm_disk.qcow2
