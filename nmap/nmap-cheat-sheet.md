# Nmap Cheat-Sheet

Uso: nmap [Tipo(s) de Varredura] [Opções] {especificação de destino}

## EXEMPLOS:

nmap -v -A scanme.nmap.org

nmap -v -sn 192.168.0.0/16 10.0.0.0/8

nmap -v -iR 10000 -Pn -p 80

VEJA A PÁGINA DE MANUAL (https://nmap.org/book/man.html) PARA MAIS OPÇÕES E EXEMPLOS

============================================================================================
## ESPECIFICAÇÃO DE DESTINO:

Pode passar nomes de host, endereços IP, redes, etc.

Ex: $nmap scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254

-iL <nome do arquivo de entrada>: Entrada da lista de hosts/redes

-iR <número de hosts>: Escolha alvos aleatórios

--exclude <host1[,host2][,host3],...>: Exclui hosts/redes

--excludefile <arquivo_de_exclusão>: Exclui lista do arquivo

======================================================================================================================
## DESCOBERTA DE HOSTS:

-sL: Varredura de Lista - simplesmente lista os alvos a serem varridos

-sn: Varredura de Ping - desabilita a varredura de portas

-Pn: Trata todos os hosts como online - ignora a descoberta de hosts

-PS/PA/PU/PY[lista_de_portas]: Descoberta de TCP SYN, TCP ACK, UDP ou SCTP para portas fornecidas

-PE/PP/PM: Sondas de descoberta de solicitações de eco ICMP, carimbo de data/hora e máscara de rede

-PO[lista_de_protocolos]: Ping de Protocolo IP

-n/-R: Nunca realiza resolução de DNS/Sempre resolve [padrão: às vezes]

--dns-servers <serv1[,serv2],...>: Especifica servidores DNS personalizados

--system-dns: Utiliza o resolvedor DNS do SO

--traceroute: Rastreia o caminho de salto para cada host

====================================================================================================================
## TÉCNICAS DE SCAN:

-sS/sT/sA/sW/sM: Scans TCP SYN/Connect()/ACK/Window/Maimon

-sU: Scan UDP

-sN/sF/sX: Scans TCP Null, FIN e Xmas

--scanflags <flags>: Personaliza os flags de scan TCP

-sI <host zumbi[:porta-sonda]>: Scan ocioso

-sY/sZ: Scans SCTP INIT/COOKIE-ECHO

-sO: Scan de protocolo IP

-b <host de retransmissão FTP>: Scan de rejeição FTP

## ESPECIFICAÇÃO DE PORTA E ORDEM DE SCAN:

-p <intervalos de portas>: Scaneia apenas portas especificadas

Ex: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9

--exclude-ports <intervalos de portas>: Exclui as portas especificadas da varredura

-F: Modo rápido - Varre menos portas do que a varredura padrão

-r: Varre as portas sequencialmente - não randomiza

--top-ports <número>: Varre <número> das portas mais comuns

--port-ratio <índice>: Varre portas mais comuns que <índice>

=======================================================================================================

## DETECÇÃO DE SERVIÇO/VERSÃO:

-sV: Sonda portas abertas para determinar informações de serviço/versão

--version-intensity <nível>: Define de 0 (leve) a 9 (teste todas as sondagens)

--version-light: Limita às sondagens mais prováveis ​​(intensidade 2)

--version-all: Tenta cada sondagem (intensidade 9)

--version-trace: Exibe a atividade detalhada da varredura de versão (para depuração)

====================================================================================================================
## VARREÇÃO DE SCRIPT:

-sC: equivalente para --script=default

--script=<scripts Lua>: <scripts Lua> é uma lista separada por vírgulas de

diretórios, arquivos de script ou categorias de script

--script-args=<n1=v1,[n2=v2,...]>: fornece argumentos para scripts

--script-args-file=nome do arquivo: fornece argumentos de script NSE em um arquivo

--script-trace: Mostra todos os dados enviados e recebidos

--script-updatedb: Atualiza o banco de dados de scripts.

--script-help=<scripts Lua>: Mostra ajuda sobre scripts.

<scripts Lua> é uma lista separada por vírgulas de arquivos de script ou
categorias de scripts.

===================================================================================================================
## DETECÇÃO DE SO:

-O: Habilita a detecção de SO

--osscan-limit: Limita a detecção de SO a alvos promissores

--osscan-guess: Adivinha o SO de forma mais agressiva

==================================================================================================================
## TEMPO E DESEMPENHO:

As opções que levam <tempo> estão em segundos ou adicionam 'ms' (milissegundos),
's' (segundos), 'm' (minutos) ou 'h' (horas) ao valor (por exemplo, 30 minutos).

-T<0-5>: Define o modelo de tempo (quanto maior, mais rápido)

--min-hostgroup/max-hostgroup <tamanho>: Tamanhos de grupos de varredura de host paralelo

--min-parallelism/max-parallelism <numprobes>: Paralelização de sondas

--min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <tempo>: Especifica
o tempo de ida e volta da sonda.

--max-retries <tentativas>: Limita o número de retransmissões da sonda de varredura de porta.

--host-timeout <tempo>: Desiste do alvo após esse tempo
--scan-delay/--max-scan-delay <tempo>: Ajusta o atraso entre as sondagens

--min-rate <número>: Envia pacotes com velocidade não inferior a <número> por segundo

--max-rate <número>: Envia pacotes com velocidade não superior a <número> por segundo

===================================================================================================================
## EVASÃO E FALSIFICAÇÃO DE MAC/IP PARA FIREWALL/IDS:

-f; --mtu <valor>: fragmenta pacotes (opcionalmente com o MTU fornecido)

-D <decoy1,decoy2[,ME],...>: mascara uma varredura com decoys

-S <endereço_IP>: falsifica o endereço de origem

-e <iface>: usa a interface especificada

-g/--source-port <núm.porta>: usa o número da porta fornecido

--proxies <url1,[url2],...>: retransmite conexões por meio de proxies HTTP/SOCKS4

--data <string hexadecimal>: adiciona um payload personalizado aos pacotes enviados

--data-string <string>: adiciona uma string ASCII personalizada aos pacotes enviados

--data-length <núm.>: adiciona dados aleatórios aos pacotes enviados

--ip-options <opções>: envia pacotes com as opções de IP especificadas

--ttl <valor>: define o campo de tempo de vida do IP

--spoof-mac <endereço MAC/prefixo/nome do fornecedor>: falsifica seu endereço MAC

--badsum: Envia pacotes com uma soma de verificação TCP/UDP/SCTP falsa 

=====================================================================================================================
## SAÍDA PARA ARQUIVOS:

-oN/-oX/-oS/-oG <arquivo>: Exibe a varredura nos formatos normal, XML, s|<rIpt kIddi3
e Grepable, respectivamente, para o nome de arquivo fornecido.

-oA <nomebase>: Saída nos três formatos principais de uma só vez

-v: Aumenta o nível de verbosidade (use -vv ou mais para maior efeito)

-d: Aumenta o nível de depuração (use -dd ou mais para maior efeito)

--reason: Exibe o motivo pelo qual uma porta está em um determinado estado

--open: Exibe apenas portas abertas (ou possivelmente abertas)

--packet-trace: Exibe todos os pacotes enviados e recebidos

--iflist: Exibe interfaces e rotas do host (para depuração)

--append-output: Anexa, em vez de sobrepor, arquivos de saída especificados

--resume <nomedoarquivo>: Retoma uma varredura abortada

--noninteractive: Desativa interações em tempo de execução via teclado

--stylesheet <caminho/URL>: Folha de estilo XSL para transformar a saída XML em HTML

--webxml: Folha de estilo de referência do Nmap.Org para XML mais portátil

--no-stylesheet: Impede a associação da folha de estilo XSL com a saída XML

=====================================================================================================================
## MISC:

-6: Habilita a varredura IPv6

-A: Habilita a detecção de SO, versão Detecção, varredura de scripts e traceroute

--datadir <nomedodiretório>: Especifica o local do arquivo de dados Nmap personalizado

--send-eth/--send-ip: Envia usando quadros Ethernet brutos ou pacotes IP

--privileged: Assume que o usuário possui privilégios completos

--unprivileged: Assume que o usuário não possui privilégios de soquete brutos

-V: Exibe o número da versão

-h: Exibe esta página de resumo de ajuda.

======================================================================================================================
