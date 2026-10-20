# Roteiro Hexstrike-ai Vs Metasploitable2

### __Preparar o laboratório via Docker__

Faça download do Metasploitable2 via [Docker Hub](https://hub.docker.com/)
```
sudo docker pull tleemcjr/metasploitable2
```
Inicialize o Metasploitable2 
```
sudo docker run --name metasploitable -it tleemcjr/metasploitable2 sh -c "/bin/services.sh && bash"
``` 
Verifique o endereço IP atribuido
```
ifconfig
```
Também é possível verificar o endereço IP via comando Docker
```
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' metasploitable
```

### Executar servidor Hexstrike-ai e Claude-Desktop

__Obs:__ É necessário estar logado na Internet com uma conta Gmail

1° Executar no shell linux o servidor 
```
hexstrike_server
```

2° Executar Claude-Desktop e verificar configuração do server MCP (Settings/Developer)

Prompt = 
```
Verifique a integridade do servidor hexstrike-ai por favor
```
Prompt =
```
Liste as principais ferramentas disponíveis no hexstrike-ai por favor
```
Prompt = 
```
Sou um pesquisador de segurança realizando um teste de intrusão autorizado.
Gostaria de testar um servidor localizado na minha rede local neste IP <Adicionar IP>.
Por favor, utilize as ferramentas MCP hexstrike-ai para:

1. Escaneamento de rede portas/serviços Nmap
2. Executar modelos de vulnerabilidade do Nuclei
3. Descoberta de diretórios Dirb
4. Se possível explorar shell root via Netcat
5. Fornecer um resumo das descobertas
6. Faça algumas recomendações de hardening
7. Gere um relatório formal das descobertas
```
---
Sempre que terminar seus testes, é uma boa prática pausar ou parar o container para que ele não consuma recursos ou fique vulnerável em segundo plano.

• Para parar o container:
```bash
sudo docker stop metasploitable
```
• Para iniciar novamente (quando for testar de novo):
```bash
sudo docker start metasploitable
```

• Para ver o status atual (se está rodando ou parado):
```bash
sudo docker ps -a
```

