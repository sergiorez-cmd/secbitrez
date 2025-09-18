# Instalar Docker-CE Debian 12 “bookworm”

Docker é um conjunto de produtos de plataforma como serviço (PaaS) que usam virtualização de nível de sistema operacional para entregar software em pacotes chamados contêineres. Os contêineres são isolados uns dos outros e agrupam seus próprios softwares, bibliotecas e arquivos de configuração. Eles podem se comunicar uns com os outros por meio de canais bem definidos. Todos os contêineres são executados por um único kernel do sistema operacional, portanto, usam menos recursos do que as máquinas virtuais. O software que hospeda os contêineres é denominado Docker Engine. Foi iniciado em 2013 e é desenvolvido pela Docker Inc.

## Adicionar GPG key oficial do Docker

`$ sudo apt update`

`$ sudo apt -y upgrade`

`$ sudo apt install -y ca-certificates curl`

`$ sudo install -m 0755 -d /etc/apt/keyrings`

`$ sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc`

`$ sudo chmod a+r /etc/apt/keyrings/docker.asc`

## Adicionar repositório oficial do Docker

`echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

## Instalar pacotes do Docker-CE

`$ sudo apt update`

`$ sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

## Testar instalação do Docker-CE

`$ sudo docker run hello-world`

## Gerenciar daemon Docker

`$ sudo systemctl [status,restart,stop,start] docker`

https://docs.docker.com/engine/install/debian/
