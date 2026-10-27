# Guia Prático de Maltego e OSINT

O **Maltego** é uma poderosa plataforma de OSINT (*Open Source Intelligence*) e análise de vínculos visuais. Ele transforma dados dispersos da internet em grafos interativos de nós e conexões, permitindo que investigadores mapeiem infraestruturas e identifiquem relações complexas.

---

## 🖥️ O que o Maltego Faz

- **Mineração de Dados e OSINT:** Coleta informações públicas e privadas em tempo real (domínios, IPs, e-mails, redes sociais, números de telefone e vazamentos).
- **Análise Gráfica (Graph):** Conecta os dados visualmente em um gráfico baseado em nós, facilitando a identificação de padrões de múltiplas ordens.
- **Módulos Principais:**
  - *Maltego Search:* Ferramenta baseada em navegador para perfis rápidos.
  - *Maltego Graph:* Análise profunda de links para grandes volumes de dados.
  - *Maltego Monitor & Evidence:* Monitoramento de mídias sociais e preservação de evidências.

### Principais Casos de Uso
- **Segurança da Informação e Pentest:** Mapeamento de infraestrutura externa de alvos.
- **Investigações Criminais e Cibercrimes:** Rastreamento de ameaças digitais e fraudes por forças de segurança.
- **Segurança Corporativa:** Avaliação de riscos na cadeia de suprimentos e exposição digital.

---

## 🎯 Tutorial: Sua Primeira Consulta (Footprinting)

Este exemplo prático demonstra como mapear o domínio de testes do projeto OWASP (`owasp.org`) para descobrir seus servidores e endereços IP.

### Passo 1: Criar um Novo Gráfico
1. Com o Maltego aberto, clique no ícone **`+` (New Graph)** no canto superior esquerdo.
2. Uma tela em branco (Workspace) se abrirá no centro da tela.

### Passo 2: Adicionar o Alvo (Entidade Domain)
1. No lado esquerdo, localize a **Palette** (paleta de entidades).
2. Procure pela categoria **Infrastructure** e arraste a entidade **Domain** (ícone de um globo) para o centro do gráfico.
3. Dê um duplo clique no texto padrão e altere para o alvo desejado: `owasp.org`.

### Passo 3: Executar a Primeira Transformação (Descobrir o IP)
No Maltego, buscas são chamadas de **Transforms** (Transformações).
1. Clique com o **botão direito** em cima do ícone do domínio `owasp.org`.
2. No menu que aparecer, procure por **DNS From Domain**.
3. Selecione a transformação **To IP Address [DNS]**.
4. O Maltego rodará a consulta e uma seta apontará do domínio para os novos nós de **endereço IP**.

### Passo 4: Expandir a Investigação
1. Clique com o **botão direito no nó de endereço IP** que surgiu no gráfico.
2. Selecione **To Location [GeoIP]** para exibir a localização geográfica e a bandeira do país de hospedagem.
3. Clique novamente com o botão direito no IP e rode **To Netblock** para revelar o bloco de rede e o provedor (ex: Cloudflare, AWS).

### Passo 5: Buscar Contatos Relacionados
1. Volte ao nó principal do domínio (`owasp.org`) e clique com o botão direito.
2. Selecione as transformações voltadas a pessoas, como **To Email Addresses [From WHOIS]**.

> 💡 **Dica de Visualização:** Conforme seu gráfico cresce, use o menu **Layout** no painel esquerdo e selecione o modo *Hierárquico* (Block Layout) para organizar os dados de cima para baixo de forma estruturada.

---

## 🔌 Instalando Transformações Gratuitas (Transform Hub)

As transformações nativas cobrem o básico. Para obter dados avançados, você deve ativar extensões no **Transform Hub**:

- **Shodan:** Descobre portas abertas, serviços ativos e vulnerabilidades nos IPs mapeados.
- **VirusTotal:** Verifica se os domínios, IPs ou e-mails estão associados a malwares ou campanhas de phishing.
- **Hunter.io:** Encontra endereços de e-mail corporativos associados a um domínio específico.

### Como Instalar:
1. Clique na aba **Transform Hub** no menu superior do Maltego.
2. Navegue pelos cards e escolha a ferramenta desejada (ex: Shodan) e clique em **Install**.
3. **Configuração de API:** Crie uma conta gratuita no site do provedor (ex: shodan.io), copie sua **API Key**, volte ao card no Maltego, clique em **Settings** e cole a chave correspondente.

---

## ⚖️ Cuidados Legais e de Privacidade (OPSEC)

A execução de inteligência de fontes abertas exige responsabilidade operacional e conformidade legal:

- **Varreduras Diretas vs. Indiretas:** Consultar bancos de dados externos (como Shodan) é considerado OSINT passivo e seguro. No entanto, transformações que fazem requisições diretas ao servidor do alvo deixam rastros nos logs de segurança do sistema investigado.
- **Uso de VPN / Tor:** Sempre utilize uma VPN confiável ou a rede Tor durante investigações para mascarar seu IP real, evitando bloqueios automáticos ou contra-inteligência pelo alvo.
- **Conformidade Legal (LGPD / RGPD):** O mapeamento de infraestrutura corporativa para fins de segurança é legítimo. Contudo, cruzar dados públicos para criar dossiês detalhados de pessoas físicas sem uma base legal válida pode violar leis de privacidade de dados.
- **Termos de Serviço:** Respeite as cotas e limites das APIs gratuitas para evitar o banimento permanente de suas chaves de acesso por automação excessiva (*scraping*).
