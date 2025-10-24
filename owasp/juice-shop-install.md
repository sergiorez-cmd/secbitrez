# Roteiro de Instalação Kali Linux + OWASP ZAP + Juice Shop

## 1° Instalar Virtualbox e Kali Linux

https://www.virtualbox.org

https://www.kali.org/get-kali/#kali-virtual-machines

https://www.kali.org/docs/virtualization/import-premade-virtualbox

## 2° Instalar Zed Attack Proxy no Kali Linux

https://www.kali.org/tools/zaproxy
```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install zaproxy -y
```
## 3° Instalar Docker-CE no Kali Linux

https://www.kali.org/docs/containers/installing-docker-on-kali
```
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list
```
```
curl -fsSL https://download.docker.com/linux/debian/gpg |
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
sudo apt update
```
```
sudo docker run hello-world
```
## 4° Deploy Juice-Shop
```
sudo docker pull bkimminich/juice-shop
```
Executar um container usando o endereço IP de localhost e acesse http://localhost:3000 
```
sudo docker run --rm -p 3000:3000 bkimminich/juice-shop
```
