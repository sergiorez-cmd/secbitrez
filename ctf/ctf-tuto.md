# Capture the Flag (CTF) no TryHackMe

Utilize o link https://markdownlivepreview.org/pt-br para visualizar o arquivo.md

Capture the Flag (CTF) no TryHackMe é uma das formas mais populares e eficientes para aprender e praticar invasão de sistemas (hacking/pentest) de forma legalizada. Nessas salas e desafios virtuais, seu objetivo é explorar vulnerabilidades em servidores para encontrar "flags" (geralmente textos no formato flag{conteúdo}) e pontuar. 


🚀 **Principais CTFs para Iniciantes (Fáceis e Gratuitos)**

Se você está começando agora, estas são as salas clássicas do tipo "boot-to-root" (onde o objetivo final é conseguir acesso de administrador/root) mais recomendadas pela comunidade: 

[beginner-friendly-ctf](https://tryhackme.com/resources/blog/your-guide-to-beginner-friendly-ctf-challenges-in-2025)

• __Simple CTF:__ Excelente para treinar escaneamento de portas básicas com Nmap e exploração de credenciais expostas.
• __RootMe:__ Focado em aplicações web. Você aprenderá a burlar filtros de upload de arquivos para conseguir uma reverse shell.
• __Pickle Rick:__ Baseado na famosa série de animação, exige o uso de injeção de comandos web (command injection) para ler arquivos ocultos.
• __Bounty Hacker:__ Ótimo para praticar força bruta (brute forcing) e exploração de má configuração do comando sudo no Linux. 


🛠️ **Metodologia Básica de Invasão em CTFs**

A maioria dos desafios de hacking segue uma estrutura lógica de passos: 

1. Reconhecimento (Recon / Port Scanning): Use ferramentas como o Nmap para descobrir quais serviços e portas estão abertos no servidor alvo (ex: porta 80 para HTTP, 21 para FTP, 22 para SSH). 

2. Enumeração de Web / Diretórios: Se houver um site rodando, use ferramentas como Gobuster ou Dirbuster para encontrar páginas ocultas que o desenvolvedor esqueceu de proteger. 

3. Exploração (Exploitation): Encontre uma vulnerabilidade (como uma versão desatualizada de um software ou falha de código) para ganhar acesso inicial ao sistema. 

4. Escalação de Privilégios (Privilege Escalation): Uma vez dentro do sistema como usuário comum, procure falhas de permissão ou arquivos SUID para se tornar o usuário supremo (root), coletando a flag final. 


💡 **Dicas de Ouro para Evoluir**

• __Aprenda a base antes:__ Fazer CTFs sem entender o básico de redes e Linux gera frustração. Se sentir dificuldade, faça a trilha teórica Pre-Security ou Cyber Security 101 no próprio site. 

• __Use os Write-ups:__ Se ficar travado por mais de 30-40 minutos em um desafio, procure um "write-up" (passo a passo) no Google ou YouTube. Aprender com a solução de outras pessoas faz parte do processo de aprendizado. 

• __Conexão:__ Lembre-se de que, para acessar as máquinas virtuais do TryHackMe, você precisa baixar o arquivo de configuração e se conectar via OpenVPN ou usar o AttackBox direto no navegador. 


## Red Team / Pentesting

Focar na área Ofensiva (Red Team / Pentesting) no TryHackMe é uma excelente escolha, pois a plataforma possui trilhas de aprendizado estruturadas que guiam você desde os conceitos mais básicos até técnicas avançadas de invasão.
Para direcionar seus estudos de forma eficiente, siga o roteiro de trilhas oficiais recomendado abaixo:


🗺️ **Roteiro de Trilhas Ofensivas no TryHackMe**

As trilhas são conjuntos de salas organizadas sequencialmente. O ideal é completá-las nesta ordem:

1. Introdução e Fundamentos

• __Introduction to Cyber Security:__ Se você é iniciante absoluto, comece por aqui. Ensina os conceitos básicos de redes, segurança web e como o hacking funciona no mundo real.
• __Pre-Security:__ Fundamental. Ensina como a internet funciona (modelo OSI, TCP/IP), conceitos cruciais de redes e comandos essenciais de Linux e Windows. Sem essa base, os desafios ofensivos ficam muito difíceis.

2. Aprendendo a Invadir (Prática Geral)

• __Junior Penetration Tester:__ A trilha mais importante para quem quer ser Pentester. Você vai aprender metodologias de invasão, ferramentas de escaneamento (Nmap), quebra de senhas (John the Ripper, Hydra), exploração de vulnerabilidades web (OWASP Top 10) e o framework Metasploit.

3. Especialização e Avançado

• __Offensive Pentesting:__ Focada em preparar você para certificações de mercado (como a OSCP). Aborda invasões mais complexas, técnicas de buffer overflow e escalação de privilégios avançada em Linux e Windows.
• __Red Teaming:__ Para quem quer simular ataques persistentes contra empresas inteiras. Ensina como burlar antivírus (EDR evasion), técnicas de pós-exploração e como atacar estruturas de Active Directory (AD).

🛠️ **Próximos Passos Práticos**

Para não ficar apenas na teoria, recomendo alternar o estudo das trilhas com a resolução daquelas salas práticas (CTFs) clássicas. Tente completar a trilha Junior Penetration Tester e, em paralelo, resolva as salas RootMe e Simple CTF usando as ferramentas que aprender lá.


🔌 **Passo 1: Conectando seu Kali ao TryHackMe (OpenVPN)**

Para atacar as máquinas do site, seu Kali precisa estar na mesma rede privada virtual deles. Siga estes passos rápidos:

1. Acesse a página tryhackme.com.
2. Certifique-se de selecionar a Região mais próxima de você (geralmente há servidores nos EUA ou Europa) para menor latência.
3. Clique em Download My Configuration File para baixar o arquivo com a extensão .ovpn.
4. No terminal do seu Kali Linux, navegue até a pasta onde baixou o arquivo e execute:
```bash
sudo openvpn seu_usuario.ovpn
```
5. Mantenha essa aba do terminal aberta. Para testar se funcionou, atualize a página de acesso do site e veja se o status mudou para conectado (com um endereço de IP no formato 10.x.x.x).

🛠️ **Passo 2: O "Kit de Sobrevivência" no Kali Linux**

Como o seu foco é a área ofensiva, existem 4 pilares de ferramentas que você usará em quase todos os CTFs e que já vêm pré-instaladas no Kali. Foque em dominar a sintaxe básica delas na trilha Junior Penetration Tester:

• __Nmap (Reconhecimento):__ Usado para descobrir o que está rodando no alvo.
	• Comando clássico: nmap -sV -sC <IP_DA_MAQUINA> (descobre versões de serviços e roda scripts padrão de vulnerabilidade).
	
• __Gobuster / Feroxbuster (Enumeração Web):__ Descobrem páginas e pastas escondidas em sites.
	• Comando clássico: gobuster dir -u http://<IP_DA_MAQUINA> -w /usr/share/wordlists/dirb/common.txt
	
• __Netcat - nc (Conexão e Reverse Shell):__ Usado para receber o controle da máquina invadida.
	• Comando clássico: nc -lvnp 4444 (coloca o seu Kali ouvindo na porta 4444 aguardando a conexão da vítima).
	
• __Hydra (Força Bruta):__ Descobre senhas de serviços como SSH, FTP ou painéis de login.
	• Comando clássico: hydra -l admin -P /usr/share/wordlists/rockyou.txt <IP> ssh

⚠️ **Dica Importante de Segurança**

Mantenha o seu Kali Linux atualizado antes de começar os laboratórios mais complexos para garantir que os exploits funcionem corretamente. No terminal, rode:
```bash
sudo apt update && sudo apt full-upgrade -y
```
## Passo a Passo do Primeiro CTF

O Hydra é uma das ferramentas mais rápidas e eficientes para ataques de força bruta (brute force). No cenário do Simple CTF, sabemos que o usuário se chama mitch (graças ao bilhete que encontramos no FTP) e que a porta SSH foi alterada para 2222.
Para descobrir a senha dele usando a wordlist clássica do Kali Linux (rockyou.txt), siga o passo a passo abaixo:

📂 **Passo 1: Preparando a Wordlist rockyou.txt**

No Kali Linux, a wordlist rockyou.txt vem compactada por padrão para economizar espaço. Se você nunca a usou, precisa descompactá-la primeiro.
Abra o terminal e execute:
```bash
sudo gunzip /usr/share/wordlists/rockyou.txt.gz
```
(Se o terminal disser que o arquivo já existe ou não foi encontrado, significa que ele já está descompactado e pronto para uso).

🚀 **Passo 2: Executando o Comando do Hydra**

Com o arquivo pronto, execute o seguinte comando no terminal (lembre-se de substituir 10.10.10.10 pelo IP real da sua máquina alvo no TryHackMe):
```bash
hydra -l mitch -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.10:2222 -t 4 -V
```

🧠 **Entendendo o comando (Sintaxe):**

• __-l mitch:__ Define o nome do usuário que estamos atacando (letra minúscula -l para um único usuário).
• __-P /usr/share/...:__ Aponta para o caminho da nossa lista de senhas (letra maiúscula -P para uma lista/arquivo).
• __ssh://10.10.10.10:2222:__ Especifica o protocolo (ssh), o IP do alvo e a porta customizada (2222), separados por dois pontos.
• __-t 4:__ Define o número de tarefas paralelas (conexões simultâneas). O SSH costuma bloquear conexões muito rápidas, então o valor 4 é seguro para não derrubar o serviço ou tomar bloqueio.
• __-V:__ Ativa o modo Verbose, que mostra na tela cada tentativa de usuário e senha que o Hydra está testando em tempo real.

🎯 **O Resultado**

O Hydra vai começar a testar centenas de senhas por segundo. Assim que ele encontrar a combinação correta, o ataque vai parar e você verá uma linha verde ou destacada parecida com esta:

text
[2222][ssh] host: 10.10.10.10   login: mitch   password: secret

Com essa senha em mãos, você pode prosseguir para o Passo 5 do guia anterior e fazer o login via SSH (ssh mitch@10.10.10.10 -p 2222).
O Hydra é uma ferramenta essencial para o seu arsenal ofensiva. Quando for testar, me avise:


