# Juice-Shop via Node.js Servidor Virtual Debian 13

Para rodar o OWASP Juice Shop em um servidor virtual Debian utilizando o Node.js diretamente (sem Docker), você precisará instalar o Node.js, instalar a versão mais recente do GitHub e iniciar o servidor. Para concluir essas tarefas é necessário ter conhecimentos sobre virtualização e criação de máquinas virtuais.

- [ ] Faça o download do Virtual Box https://www.virtualbox.org

- [ ] Faça o download da imagem de instalação do Debian 13 https://www.debian.org

- [ ] Instale o Virtual Box, em seguida crie uma máquina virtual com a imagem do Debian 13

- [ ] Configure a placa de rede do Virtual Box para modo bridge e atribua um IP fixo para o Debian 13 conforme seu ambiente

https://secbitrez.wordpress.com/labs

https://github.com/sergiorez-cmd/secbitrez/blob/main/shell-linux/essential-linux.md

## 1. Atualizar o sistema e instalar dependências básicas

Acesse o seu servidor Debian via SSH e execute os comandos abaixo para garantir que o sistema esteja atualizado e com as ferramentas necessárias instaladas:
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install git curl build-essential -y
```

## 2. Instalar o Node.js

O OWASP Juice Shop requer uma versão recente do Node.js (atualmente as versões LTS 22, 24 ou 26 funcionam perfeitamente). Vamos instalar a versão estável mais recomendada utilizando o site oficial:

https://nodejs.org/pt-br

### Procedimento para instalar a versão 26.13.0 LTS
```bash
# Baixar e instalar o nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# Carregar o nvm sem precisar reiniciar o shell
\. "$HOME/.nvm/nvm.sh"

# Baixar e instalar o Node.js:
nvm install 26

# Verifique a versão do Node.js:
node -v # Deve exibir "v26.13.0".

# Verificar a versão do npm:
npm -v # Deve imprimir "11.20.0".
```
---

## 3. Baixar e Configurar o Juice Shop

https://github.com/juice-shop/juice-shop

Faça o download juice-shop-<version>_<node-version>_<os>_x64.zip(ou acesse .tgz) o link anexado à versão mais recente.

https://github.com/juice-shop/juice-shop/releases/tag/v20.3.0
```bash
wget -c https://github.com/juice-shop/juice-shop/releases/download/v20.3.0/juice-shop-20.3.0_node26_linux_x64.tgz
```
Descompacte o arquivo.
```bash
tar -xvzf juice-shop-20.3.0_node26_linux_x64.tgz
```
Executar o Juice-Shop `cd juice-shop_20.3.0` e `npm start`

Acesse via browser `http://<IP_Debian13>:3000`


### 💡 Dicas importantes para Servidores Virtuais (VPS)

• __Liberar a porta no Firewall:__ Se você estiver usando um provedor como AWS, DigitalOcean ou Google Cloud, lembre-se de liberar a porta 3000 nas configurações de rede/firewall do painel da sua VPS.

• __Rodar em segundo plano (PM2):__ Se você fechar o terminal SSH, o Juice Shop irá parar. Para mantê-lo rodando para sempre em segundo plano, utilize o gerenciador de processos pm2:bash
```bash
sudo npm install -g pm2
```
```bash
pm2 start app.js --name "juice-shop"
```
• __Acesso seguro:__ Por se tratar de uma aplicação intencionalmente vulnerável, não a deixe exposta publicamente na internet por muito tempo sem proteção ou sem restringir o acesso ao seu IP no firewall, para evitar que terceiros abusem do seu servidor.


## Realizar Auditoria de Segurança Via NPM Audit

Para executar uma auditoria de segurança diretamente no repositório do OWASP Juice Shop usando o gerenciador de pacotes, basta utilizar o comando nativo do NPM. Como o Juice Shop é um laboratório intencionalmente vulnerável, o resultado trará um número massivo de falhas conhecidas.

Execute o comando abaixo dentro da pasta do projeto (juice-shop):
```bash
npm audit
```

**📊 O que esperar do resultado?**

Ao rodar esse comando no Juice Shop, o terminal exibirá um relatório detalhado contendo:
• __Total de vulnerabilidades:__ Divididas por severidade (Low, Moderate, High, Critical).
• __ID do Advisory:__ Links ou códigos de referência para bases de dados de vulnerabilidades (como a GitHub Advisory Database).
• __Caminho da dependência:__ Qual pacote principal ou subdependência está vulnerável.
• __Descrição da falha:__ O tipo de ataque que ela permite (ex: Remote Code Execution, Denial of Service, Prototype Pollution).

**⚠️ Cuidados ao usar o npm audit fix neste laboratório**

Em projetos reais de desenvolvimento, o comando comum para corrigir as falhas automaticamente é o `npm audit fix`. No entanto, não é recomendado fazer isso no Juice Shop, a menos que o seu objetivo seja justamente estudar como o código quebra ou se comporta após as correções.

### NÃO RECOMENDADO para o funcionamento padrão do lab:
```bash
npm audit fix
```
Isso atualizará os pacotes para versões seguras, o que vai corrigir e sumir com vários dos desafios de "hacking" que fazem parte da proposta didática do Juice Shop, além de poder quebrar a compatibilidade interna do ecossistema do laboratório.

## CVE Lite CLI

https://owasp.github.io/cve-lite-cli

Varredura de vulnerabilidades que começa no seu terminal e se integra perfeitamente ao CI.
Analise seu arquivo de dependências (lockfile), obtenha comandos de correção prontos para copiar e executar, e entregue um código seguro.

O CVE Lite CLI foi projetado com foco em ciclos curtos de feedback local: analisar um arquivo de bloqueio (lockfile), identificar se as vulnerabilidades encontradas são diretas ou transitivas, aplicar o comando de correção mais seguro disponível e realizar uma nova análise antes que o código chegue à CI.
```bash
npm install -g cve-lite-cli
```
```bash
cve-lite /path/to/project --verbose
```

__Opções:__
```bash
cve-lite /path/to/project                   # basic scan
cve-lite /path/to/project --verbose         # full fix plan with dependency paths
cve-lite /path/to/project --fix             # apply validated direct fixes and rescan
cve-lite /path/to/project --fail-on high    # exit non-zero on high severity and above
cve-lite /path/to/project --json            # JSON output
cve-lite /path/to/project --sarif           # SARIF output for GitHub Code Scanning
cve-lite /path/to/project --sbom spdx       # SPDX 2.3 SBOM (also: --sbom cyclonedx)
cve-lite /path/to/project --sarif --output reports # write output files into ./reports
cve-lite /path/to/project --report          # interactive HTML dashboard
cve-lite /path/to/project --check-overrides # audit override hygiene alongside the CVE scan
cve-lite /path/to/project --check-maintenance # flag CVE-blocking version drag and npm-deprecated direct deps
cve-lite /path/to/project --check-licenses  # detect copyleft and unknown licenses alongside the CVE scan
cve-lite advisories sync                    # sync advisory DB for offline use
cve-lite advisories init                    # create an empty advisory DB to populate yourself
cve-lite /path/to/project --offline         # scan with no runtime API calls
```
__Lista completa de opções:__
https://owasp.github.io/cve-lite-cli/docs/cli-reference
