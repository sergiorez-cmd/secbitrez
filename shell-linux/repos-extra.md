## Adicionar repositórios extras

$ sudo nano /etc/apt/sources.list

Adicionar no final das linhas

contrib non-free


## Ativar Flatpacks

$ sudo apt install flatpak -y

$ sudo apt install gnome-software-plugin-flatpak -y

$ flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

https://flashhub.org/setup/Debian

## Repositório  Oracle Virtual Box Debian

$ wget -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc | sudo gpg --yes --output /usr/share/keyrings/oracle-virtualbox-2016.gpg --dearmor

$ sudo apt update

$ sudo apt install virtualbox-7.1
