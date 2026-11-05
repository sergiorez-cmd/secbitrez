# Install Docker Debian 13 Trixie


## Requisitos do sistema operacional para instalação do Docker-CE

Para instalar o Docker Engine, você precisa de uma destas versões do Debian:

* **Debian Trixie 13 (estável)**

* **Debian Bookworm 12 (oldstable)**

O Docker Engine para Debian é compatível com as arquiteturas x86_64 (ou amd64), armhf (arm/v7), arm64 e ppc64le (ppc64el).

Antes de instalar o Docker Engine pela primeira vez em uma nova máquina host, você precisa configurar o `apt` repositório do Docker. Depois disso, você poderá instalar e atualizar o Docker a partir do repositório.

- [ ] Instale as chaves de assinatura GPG do Docker
```bash
# Add Docker's official GPG key:
sudo apt update
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
- [ ] Configure apt repositório do Docker.
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
```bash
# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```
- [ ] Atualize os repositórios do Debian 13
```bash
sudo apt update
```
- [ ] Instale os pacotes necessários do Docker-CE
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
- [ ] Inicialize o Docker-CE e teste
```bash
sudo systemctl status docker
```
```bash
sudo systemctl start docker
```
```bash
sudo docker run hello-world
```
https://docs.docker.com/engine/install/debian/#os-requirements
---

## Usando a Imagem Docker Oficial do Ollama

O Docker oferece uma maneira agnóstica de plataforma para executar o Ollama em um contêiner isolado, simplificando o gerenciamento de dependências, especialmente para configurações complexas de GPU.

**Contêiner Ollama Apenas CPU:**
```bash
sudo docker pull ollama/ollama
```
```bash
sudo docker run -d -v ollama_data:/root/.ollama -p 11434:11434 --name my_ollama ollama/ollama
```

* **-d:** Executa o contêiner em modo detached (segundo plano).

* **-v:** ollama_data:/root/.ollama: Cria um volume nomeado do Docker chamado ollama_data em seu sistema host e o mapeia para o diretório /root/.ollama dentro do contêiner. Isso é crucial para persistir seus modelos baixados. Se omitir isso, os modelos serão perdidos quando o contêiner for removido. Você pode escolher qualquer nome para o volume.

* **-p:** 11434:11434: Mapeia a porta 11434 na interface loopback da sua máquina host (127.0.0.1) para a porta 11434 dentro do contêiner. Use 0.0.0.0:11434:11434 se precisar acessar o contêiner Ollama de outras máquinas em sua rede.

* **--name** my_ollama: Atribui um nome personalizado e memorável ao contêiner em execução.
ollama/ollama: Especifica a imagem oficial do Ollama do Docker Hub.

https://hub.docker.com/r/ollama/ollama
