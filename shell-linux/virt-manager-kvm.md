# KVM Virt-manager Debian 12/13

## 1° Instalar pacotes
```bash
grep -E --color '(vmx|svm)' /proc/cpuinfo
```
```bash
sudo apt update
```
```bash
sudo apt install -y qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
```
```bash
systemctl status libvirtd
``` 
```bash
sudo systemctl enable --now libvirtd
```
```bash
lsmod | grep -i kvm
```
## 2° Ativar rede virtual
```bash
sudo virsh net-start default
```
```bash
sudo virsh net-autostart default
```
```bash
sudo virsh net-list --all
``` 
## 3° Criar uma rede local bridge
```bash
sudo nano /etc/network/interfaces
```
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
```bash
sudo systemctl restart networking.service
```
## Converter discos virtuais 
```bash
sudo apt install qemu-utils
```
```bash
tar -xvf vm_disk.ova
```
```bash
qemu-img convert -p -f vmdk -O qcow2 vm_disk.vmdk new_vm_disk.qcow2
```
```bash
qemu-img convert -p -f vhdx -O qcow2 /virtual_disk_directory/vm_disk.vhdx /disk_directory/new_vm_disk.qcow2
``
