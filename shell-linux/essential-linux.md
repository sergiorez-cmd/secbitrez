# Linux Configurações Essenciais de Servidores

## 1° Atualizar pacotes do sistema operacional

### ============================================

Debian/Ubuntu
```
apt update && apt upgrade -y
```
RHEL/Rocky/Oracle
```
dnf update -y
```
Adicionar repositório opcional em sistemas RHEL
```
dnf install epel-release -y
```

## 2° Usuário administrador (sudoers/sudo su)

### ==========================================

Debian/Ubuntu
```
apt install sudo -y (Somente Debian)
```
```
usermod -aG sudo name_user
```
RHEL/Rocky/Oracle
```
usermod -aG wheel name_user
```
Arquivo Sudoers para configuração de privilégios administrativos
```
/etc/sudoers
```
Editar arquivo Sudoers
```
visudo -f /etc/sudoers
```
Adicionar um grupo específico para fins administrativos
```
%admgrp ALL=(ALL) ALL
```
Verificar usuários do grupo Sudoers
``` 
grep ‘sudo’ /etc/group
```
```
getent group wheel
```

## 3° Verificar firewall do sistema

### =================================

Debian/Ubuntu
```
ufw status
ufw status verbose
ufw [enable|disable]
ufw default deny incoming
ufw default allow outgoing
ufw app list
ufw allow 'OpenSSH'
ufw allow 22/tcp
```
RHEL/Rocky/Oracle
```
firewall-cmd --state
firewall-cmd --permanent --list-all
firewall-cmd --get-services
firewall-cmd --permanent --add-port=22/tcp
firewall-cmd --permanent --add-service=ssh
firewall-cmd --reload
systemctl [start|stop] firewalld
systemctl [enable|disable] firewalld
```

## 4° Configurações de rede (nome de host, endereço IP, gateway, servidores DNS)

#### ============================================================================

Debian 12 (Edição Manual)
```
nano /etc/network/interfaces
```
```
iface enp0s3 inet static
address 192.168.1.10
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
gateway 192.168.1.1
```
```
systemctl restart networking
```
```
nano /etc/resolv.conf
```
```
nameserver 9.9.9.9
nameserver 149.112.112.112
```
```
hostnamectl set-hostname server1
```
Ubuntu 24 (Edição Manual)
```
#vim /etc/netplan/50-cloud-init.yaml
```
```
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
```
netplan try
```
```
netplan apply
```

RHEL9/Rocky9/Oracle9
```
nmtui (modo visual)
```
```
nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
```
``` 
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.3.20
PREFIX=24
GATEWAY=192.168.3.1
DNS1=208.67.222.222
DNS2=208.67.220.220
```

## 5° Instalar e configurar Fail2Ban para proteção SSH

### =====================================================
```
sudo apt install fail2ban -y
```
Configurar Fail2Ban para proteção SSH
```
sudo nano /etc/fail2ban/jail.local
```
```
[sshd]
enabled = true
port = ssh
logpath = %(sshd_log)s
maxretry = 3
bantime = 3600
```
Reiniciar Fail2Ban para aplicar a configuração
```
sudo systemctl restart fail2ban
```
```
fail2ban-client status
```

## 6° Criar um par de chaves RSA para acesso SSH sem senha

### ==========================================================

RHEL/Rocky/Oracle
```
ssh-keygen
```
Diretório das chaves RSA
```
/home/user_name/.ssh/id_rsa
```
Copiar chave RSA para servidor remoto
```
ssh-copy-id username@remote_host
```
Acessar servidor remoto via SSH
```
ssh user_name@remote_IP
```
Desativar autenticação de senhas SSH
```
sudo nano /etc/ssh/sshd_config
```
Editar linha
```
PasswordAuthentication no
```
Reiniciar configuração de serviços
``` 
sudo systemctl daemon-reload
```

## 7° Atualizações de segurança automáticas Debian/Ubuntu

### =======================================================

Debian/Ubuntu
```
sudo apt install unattended-upgrades -y
```
```
sudo dpkg-reconfigure -plow unattended-upgrades
```
```
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```
``` 
sudo systemctl status unattended-upgrades.service
```

RHEL/Oracle/Rocky Linux
```
dnf install dnf-automatic -y
```
```
nano /etc/dnf/automatic
```
```
upgrade_type = security
```
```
systemctl enable dnf-automatic-install.timer
```
```
systemctl status dnf-automatic-install
```

## 8° Instalar Htop para monitorar processos e recursos do sistema

### ================================================================

Debian/Ubuntu
```
$sudo apt install -y htop
```

Oracle/Rocky Linux
```
dnf install epel-release
```
```
dnf install -y htop
```

## 9° Habilitar Painel de Gerenciamento Cockpit Debian/Rocky Linux

## ================================================================
```
sudo apt install -y cockpit
```
```
sudo dnf install -y cockpit
```
```
sudo systemctl enable --now cockpit.socket
```
```
sudo systemctl start cockpit
```
https://cockpit-project.org/running
