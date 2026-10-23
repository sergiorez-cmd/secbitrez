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

1. Escaneamento de rede, todas portas TCP via Nmap
2. Executar modelos de vulnerabilidades CVE do Nuclei
3. Descoberta de diretórios comuns via Feroxbuster
4. Explorar shell root, se encontrar vulnerabilidades
5. Fornecer um resumo das descobertas
6. Faça algumas recomendações de hardening
7. Gere um relatório formal das descobertas
```
Prompt = 
```
Explore a porta 1524 com o serviço ingreslock
```
Prompt = 
```
Verifique a vulnerabilidade distccd (3632) com script do Nmap
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
• Para acessar o container:
```bash
sudo docker attach metasploitable
```
• Para ver o status atual (se está rodando ou parado):
```bash
sudo docker ps
```
• Também é possível verificar o endereço IP via comando Docker
```
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' metasploitable
```

# Roteiro Hexstrike-ai Vs Juice-Shop

Inicialize o Juice-Shop
```
sudo docker run --rm -p 3000:3000 bkimminich/juice-shop
```
Prompt = 

```
Sou um pesquisador de segurança e gostaria de testar as ferramentas do hexstrike-ai.
A aplicação alvo esta rodando em uma estância do juice-shop via docker da minha máquina local.
Execute a sequência de testes no caminho http://localhost:3000: 

1. Recon via Nmap na porta 3000.
2. Não está autorizado realizar força bruta de diretórios.
3. Executar o Nikto com escopo/tempo para evitar timeout longo e focado nas falhas de injeção (XSS/SQLi).
4. Rodar o SQLmap diretamente via shell e testar (/rest/products/search?q=q).
5. Realize uma análise da chave JWT.
6. Testar a API REST.
7. Gere um relatório formal das descobertas.
```
