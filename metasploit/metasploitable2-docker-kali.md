# Metasploitable2 no Kali Linux via Docker

### Instalar e Executar

Para rodar uma instância do Metasploitable no Docker dentro do Kali Linux, você só precisa garantir que o Docker esteja instalado e executar uma imagem pré-configurada do Metasploitable 2.

__Passo 1: Instalar e iniciar o Docker__

Caso ainda não tenha o Docker instalado no seu Kali Linux, abra o terminal e execute:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
```

__Passo 2: Baixar e rodar o Metasploitable2__

A imagem mais popular e pronta para uso da comunidade é a tleemcjr/metasploitable2 [0.6.1]. Execute o comando abaixo para baixar e iniciar o container:

```bash
sudo docker pull tleemcjr/metasploitable2
``` 
```bash
sudo docker run --name metasploitable -it tleemcjr/metasploitable2 sh -c "/bin/services.sh && bash"
```

__O que este comando faz:__

• __-d:__ Roda o container em segundo plano (background).
• __--name metasploitable__: Dá um nome amigável ao container.
• __-p [porta:porta]__: Mapeia as portas vulneráveis do container (FTP, SSH, Telnet, HTTP, SMB, PostgreSQL) para a sua máquina Kali, permitindo que você as ataque diretamente via localhost ou pelo IP da sua máquina.

__Passo 3: Verificar se está rodando__

Para confirmar que o container está ativo e ver quais portas estão abertas, utilize:

```bash
sudo docker ps
```

Se precisar descobrir o IP interno do container para simular um ataque em rede local, use:

```bash
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' metasploitable
```

Agora você já pode abrir o Metasploit Framework (msfconsole) ou o Nmap no seu Kali Linux e apontar para o IP gerado ou para o seu próprio localhost.

### Rede Isolada e Gerenciamento

Para gerenciar seu laboratório com segurança, o ideal é criar uma rede isolada no Docker (Bridge Network). Isso evita que os serviços vulneráveis do Metasploitable fiquem expostos à sua rede física local, mantendo o tráfego de ataque restrito ao ambiente virtualizado.

1. __Criando uma Rede Isolada no Docker__

Primeiro, vamos criar uma rede customizada chamada lab_pentest:

```bash
sudo docker network create lab_pentest
```

Agora, vamos remover o container antigo (se ainda estiver rodando) e iniciar um novo conectado diretamente a essa rede. Dessa forma, você não precisa expor as portas para a sua máquina hospedeira (sem o parâmetro -p), pois o Kali e o Metasploitable vão se comunicar dentro da rede interna do Docker

__Para remover o container anterior__
```bash
sudo docker rm -f metasploitable
```
__Para rodar o novo na rede isolada__
```
sudo docker run -d --name metasploitable --network lab_pentest tleemcjr/metasploitable2
```

2. __Como Interagir (Descobrir o IP para Ataque)__

Como o container está em uma rede isolada, você precisa descobrir o IP interno dele para que o Metasploit ou o Nmap possam encontrá-lo:

```bash
sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' metasploitable
```
O retorno será um IP interno (ex: 172.18.0.2). Use este IP como seu RHOSTS no Metasploit.

__Entrando no terminal do Metasploitable (Modo Interativo)__

Se você precisar acessar o terminal do próprio Metasploitable para verificar logs, configurações ou arquivos, use:
```bash
sudo docker exec -it metasploitable /bin/bash
```

3. __Gerenciando o Container (Parar e Reiniciar)__

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

