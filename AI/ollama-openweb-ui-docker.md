# Ollama + Open WebUI no Debian 13

No Debian 13, o comando oficial do Docker moderno utiliza docker compose. 

Siga o passo a passo:

1. Criar a estrutura e o arquivo

No seu Debian 13, crie a pasta do projeto e o arquivo de configuração:

```bash
mkdir -p ~/ollama-webui
cd ~/ollama-webui
gnome-text-editor docker-compose.yml
```

### Cole o conteúdo abaixo dentro do arquivo:
```text
services:
  # Servidor LLM Local
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    volumes:
      - ollama_data:/root/.ollama
    ports:
      - "11434:11434"
    restart: always

  # Interface Web para Interação Manual e Testes
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    volumes:
      - open_webui_data:/app/backend/data
    depends_on:
      - ollama
    ports:
      - "3000:8080"
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
    restart: always

volumes:
  ollama_data:
  open_webui_data:

```

2. Iniciar os serviços

Execute o comando para baixar as imagens e iniciar os contêineres em segundo plano:
```bash
sudo docker compose up -d
```

3. Baixar um modelo leve para testar

Para garantir que tudo funcione rápido no Debian 13, use o próprio Docker para mandar o Ollama baixar o modelo Llama 3.2 (que é leve e excelente para testes):
```bash
sudo docker exec -it ollama ollama run llama3.2:1b
```
Assim que o download terminar e abrir o chat no terminal, você pode digitar /exit para sair.

4. Acessar a interface gráfica

Abra o navegador no seu Debian (ou em qualquer máquina da mesma rede local usando o IP do servidor) e acesse:
```text
http://localhost:3000
```
Crie sua conta de administrador (os dados ficam salvos localmente na sua máquina) e o modelo llama3.2 já estará disponível no topo da tela para seleção.

### Gerenciar containers 

Para parar os seus containers, execute um dos comandos abaixo diretamente no terminal, dentro da pasta onde está o seu arquivo docker-compose.yml:

⏹️ Apenas parar (mantém os dados e containers salvos)

Para interromper a execução sem apagar nada:
```bash
sudo docker compose stop
```

🧹 Parar e remover (limpa os containers e redes)

Para encerrar e excluir os containers criados pelo Compose, liberando memória:
```bash
sudo docker compose down
```

🗂️ Limpeza total (remover containers e volumes de dados)

Se além dos containers você também quiser apagar os volumes de dados criados por eles (zerar o banco de dados, por exemplo):
```bash
sudo docker compose down -v
```
---

## Configuração 100% otimizada para o Debian 13 com GPU Dedicada NVIDIA:

• A máquina possui GPU dedicada da NVIDIA? (Se sim, precisamos adicionar as linhas de aceleração de hardware no arquivo).

Para que o contêiner do Docker consiga "conversar" com a sua placa de vídeo no Debian 13, você precisará instalar o NVIDIA Container Toolkit no sistema operacional hospedeiro antes de subir o Docker Compose. 

Siga estes passos rápidos no terminal do seu Debian 13:

* **Passo 1:** Instalar o NVIDIA Container Toolkit no Debian 13

Caso você ainda não tenha feito isso, adicione o repositório oficial da NVIDIA e instale a ferramenta de integração com o Docker: 

1. Adicione a chave GPG e o repositório:bash
```bash
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
```
```bash
curl -fsSL https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

2. Atualize os pacotes e instale o toolkit:
```bash
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
```

3. Configure o Docker para reconhecer o runtime da NVIDIA e reinicie o serviço (essencial para aplicar a mudança): 
```bash
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```
* **Passo 2:** Atualizar o seu docker-compose.yml

Agora, modifique o arquivo que criamos anteriormente para injetar o suporte a hardware (deploy) na imagem do Ollama: 

yaml
```text
services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    volumes:
      - ollama_data:/root/.ollama
    ports:
      - "11434:11434"
    restart: always
    # Bloco que ativa o uso da GPU NVIDIA dentro do container:
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]

  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    volumes:
      - open_webui_data:/app/backend/data
    depends_on:
      - ollama
    ports:
      - "3000:8080"
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
    restart: always

volumes:
  ollama_data:
  open_webui_data:
```
* **Passo 3:** Reiniciar a Stack e Validar

1. Suba os contêineres atualizados:
```bash
sudo docker compose up -d
```

2. Para ter a certeza absoluta de que o Ollama está enxergando a sua GPU através do Docker, rode este comando de diagnóstico:
```bash
sudo docker exec -it ollama nvidia-smi
```

Se ele exibir o painel da sua placa de vídeo (mostrando o nome da GPU e o consumo de VRAM), a aceleração está funcionando perfeitamente! 

Próximo Passo Recomendado

Visto que você possui uma GPU, você não precisa ficar preso apenas a modelos super leves. Você já pode baixar modelos muito mais robustos diretamente na interface Web ou pelo terminal: 

• **Llama 3.1 (8B):** docker exec -it ollama ollama run llama3.1 (Excelente para tarefas gerais e programação).

• **Mistral (7B):** docker exec -it ollama ollama run mistral (Ótimo raciocínio técnico).




