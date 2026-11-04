# Linux Configurações Essenciais de Servidores

## 1° Atualizar pacotes do sistema operacional

Debian/Ubuntu
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt autoremove -y && sudo apt autoclean
```
RHEL/Rocky/Oracle
```bash
dnf update -y
```
Adicionar repositório opcional em sistemas RHEL
```
dnf install epel-release -y
```

## 2° Usuário administrador (sudoers/sudo su)

Debian/Ubuntu
```bash
apt install sudo -y (Somente Debian)
```
```bash
sudo usermod -aG sudo name_user
```
RHEL/Rocky/Oracle
```bash
usermod -aG wheel name_user
```
Arquivo Sudoers para configuração de privilégios administrativos
```text
/etc/sudoers
```
Editar arquivo Sudoers
```bash
visudo -f /etc/sudoers
```
Adicionar um grupo específico para fins administrativos
```text
%admgrp ALL=(ALL) ALL
```
Verificar usuários do grupo Sudoers
```bash
grep ‘sudo’ /etc/group
```
```bash
getent group wheel
```

## 3° Verificar firewall do sistema

Debian/Ubuntu
```bash
ufw status
ufw status verbose
ufw [enable|disable]
ufw default deny incoming
ufw default allow outgoing
ufw app list
ufw allow 'OpenSSH'
ufw allow 22/tcp
ufw allow 9090/tcp
ufw reload
```
RHEL/Rocky/Oracle
```bash
firewall-cmd --state
firewall-cmd --permanent --list-all
firewall-cmd --get-services
firewall-cmd --permanent --add-port=22/tcp
firewall-cmd --permanent --add-service=ssh
firewall-cmd --permanent --add-service=cockpit
firewall-cmd --reload
systemctl [start|stop] firewalld
systemctl [enable|disable] firewalld
```

## 4° Configurações de rede (nome de host, endereço IP, gateway, servidores DNS)

Debian 12 (Edição Manual)
```bash
nano /etc/network/interfaces
```
```text
iface enp0s3 inet static
  address 192.168.1.10
  netmask 255.255.255.0
  network 192.168.1.0
  broadcast 192.168.1.255
  gateway 192.168.1.1
```
```bash
systemctl restart networking
```
```bash
nano /etc/resolv.conf
```
```text
nameserver 9.9.9.9
nameserver 149.112.112.112
```
```bash
hostnamectl set-hostname server1
```
Ubuntu 24 (Edição Manual)
```bash
vim /etc/netplan/50-cloud-init.yaml
```
```text
network:
ethernets:
enp0s3:
dhcp4: false
addresses: [192.168.1.10/24]
nameservers:
addresses: [9.9.9.9,149.112.112.112]
routes:
- to: default
via: 192.168.1.1
```
version: 2
```bash
netplan try
```
```bash
netplan apply
```

RHEL9/Rocky9/Oracle9
```bash
nmtui (modo visual)
```
```bash
nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
```
``` text
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.3.20
PREFIX=24
GATEWAY=192.168.3.1
DNS1=208.67.222.222
DNS2=208.67.220.220
```

## 5° Instalar e configurar Fail2Ban para proteção SSH

```bash
sudo apt install -y fail2ban
```
Configurar Fail2Ban para proteção SSH
```bash
sudo nano /etc/fail2ban/jail.local
```
```text
[sshd]
enabled = true
port = ssh
logpath = %(sshd_log)s
maxretry = 3
bantime = 3600
```
Reiniciar Fail2Ban para aplicar a configuração
```bash
sudo systemctl restart fail2ban
```
```bash
fail2ban-client status
```

## 6° Criar um par de chaves RSA para acesso SSH sem senha


RHEL/Rocky/Oracle
```bash
ssh-keygen
```
Diretório das chaves RSA
```bash
/home/user_name/.ssh/id_rsa
```
Copiar chave RSA para servidor remoto
```bash
ssh-copy-id username@remote_host
```
Acessar servidor remoto via SSH
```bash
ssh user_name@remote_IP
```
Desativar autenticação de senhas SSH
```bash
sudo nano /etc/ssh/sshd_config
```
Editar linha
```text
PasswordAuthentication no
```
Reiniciar configuração de serviços
```bash
sudo systemctl daemon-reload
```

## 7° Atualizações de segurança automáticas Debian/Ubuntu

Debian/Ubuntu
```bash
sudo apt install -y unattended-upgrades
```
```bash
sudo dpkg-reconfigure -plow unattended-upgrades
```
```bash
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```
```bash
sudo systemctl status unattended-upgrades.service
```

RHEL/Oracle/Rocky Linux
```bash
dnf install -y dnf-automatic
```
```bash
vim /etc/dnf/automatic.conf
```
Alterar o tipo de atualização somente para segurança
```text
upgrade_type = security
```
```bash
systemctl enable dnf-automatic-install.timer
```
```bash
systemctl status dnf-automatic-install
```

## 8° Instalar Htop para monitorar processos e recursos do sistema

Debian/Ubuntu
```bash
sudo apt install -y htop
```

Oracle/Rocky Linux
```bash
dnf install epel-release
```
```bash
dnf install -y htop
```

## 9° Habilitar Painel de Gerenciamento Cockpit Debian/Rocky Linux

```bash
sudo apt install -y cockpit
```
```bash
sudo dnf install -y cockpit
```
```bash
sudo systemctl enable --now cockpit.socket
```
```bash
sudo systemctl start cockpit
```
https://cockpit-project.org/running
