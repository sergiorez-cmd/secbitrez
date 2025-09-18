# Instalando Docker-CE no Kali Linux

$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list

https://www.kali.org/docs/containers/installing-docker-on-kali
