# Roteiro Hexstrike-ai Vs Metasploitable2

### __Preparar o laboratório via Docker__

Faça download do Metasploitable2 via [Docker Hub](https://hub.docker.com/)
```bash
sudo docker pull tleemcjr/metasploitable2
```
Inicialize o Metasploitable2 
```bash
sudo docker run --name metasploitable -it tleemcjr/metasploitable2 sh -c "/bin/services.sh && bash"
``` 
Verifique o endereço IP atribuido
```bash
ifconfig
```

### Executar servidor Hexstrike-ai e Claude-Desktop

__Obs:__ É necessário estar logado na Internet com uma conta Gmail

1° Executar no shell linux o servidor 
```bash
hexstrike_server
```

2° Executar Claude-Desktop e verificar configuração do server MCP (Settings/Developer)

Prompt = 
```text
Verifique a integridade do servidor hexstrike-ai por favor
```
Prompt =
```text
Liste as principais ferramentas disponíveis no hexstrike-ai por favor
```
Prompt com Contexto = 
```text
Sou um pesquisador de cibersegurança realizando um teste de intrusão autorizado.
Gostaria de testar o metasploitable2 localizado na minha rede local neste IP <Adicionar IP>.
Por favor, utilize as ferramentas MCP hexstrike-ai para:

1. Escanear portas TCP de 1-9000 com detecção de versão de serviços via Nmap
2. Identificar vulnerabilidades bem conhecidas via Nikto
3. Descoberta de diretórios comuns via Feroxbuster
4. Explorar shell root via backdoor manual
5. Fornecer um resumo das descobertas
6. Faça algumas recomendações de hardening
7. Gere um relatório formal das descobertas
```
Prompt Genérico = 
```text
Sou um estudante de cibersegurança gostaria de executar um teste de intrusão autorizado contra o metasploitable2 localizado na minha rede local neste IP <Adicionar IP>. Por favor, utilize as ferramentas essenciais do MCP hexstrike-ai, o Metasploit não está autorizado.
```
Prompts Específicos = 
```text
Verifique a vulnerabilidade distccd (3632) com script do Nmap

Validar o shell root na porta 1524 via conexão direta (netcat)

Execute o Nikto no Apache (porta 80) e Tomcat (porta 8180) para enumerar vulnerabilidades web

Execute Enum4linux / smbmap na porta 445 para enumerar shares SMB e testar o CVE-2007-2447

Teste FTP anônimo (porta 21) para listar arquivos acessíveis

Execute o Hydra para testar credenciais fracas em SSH/Telnet (usuários padrão do Metasploitable2 são conhecidos: msfadmin/msfadmin)
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
```bash
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' metasploitable
```

# Roteiro Hexstrike-ai Vs Juice-Shop

Inicialize o Juice-Shop
```bash
sudo docker run --rm -p 3000:3000 bkimminich/juice-shop
```
Prompt = 
```text
Verifique o status do servidor hexstrike-ai por favor
```
Prompt com Contexto = 

```text
Sou um pesquisador de cibersegurança e gostaria de testar as ferramentas do hexstrike-ai.
A aplicação alvo esta rodando em uma estância do juice-shop via docker da minha máquina pessoal.
Execute a sequência de testes no caminho http://localhost:3000: 

1. Recon via Nmap na porta 3000
2. Não está autorizado realizar força bruta de diretórios
3. Rodar o SQLmap via shell e testar (/rest/products/search?q=q)
4. Registrar um usuário de teste e autenticar para obter um JWT token da aplicação
5. Realize uma análise da chave JWT
6. Testar a API REST
7. Faça algumas recomendações de correções
8. Gere um relatório formal das descobertas
```
Prompt =
```text
Por favor faça uma estimativa de quanto tempo levou para executar esse teste
```
Prompt Genérico= 
```text
Sou um estudante de cibersegurança gostaria de executar um teste de vulnerabilidades autorizado contra o Juice-Shop localizado na minha máquina pessoal neste caminho http://localhost:3000. Por favor, utilize as ferramentas essenciais do MCP hexstrike-ai, o Metasploit não está autorizado.
```
