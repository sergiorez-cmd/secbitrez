# Instalando Docker-CE no Kali Linux
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list
```
```
`$ curl -fsSL https://download.docker.com/linux/debian/gpg`

`$ sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`

`$ sudo apt update`

`$ sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

`$ sudo docker run hello-world`
```
https://www.kali.org/docs/containers/installing-docker-on-kali
