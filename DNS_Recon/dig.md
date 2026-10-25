# DNS Dig

O comando **`dig`** (Domain Information Groper) é uma das ferramentas mais versáteis e utilizadas por administradores de sistemas e desenvolvedores para diagnosticar e consultar informações de DNS.

Abaixo estão os principais comandos e opções organizados por categoria para facilitar o seu dia a dia:

---

## 1. Consultas Básicas e por Tipo de Registro

Por padrão, ao executar o comando sem especificar o tipo, o `dig` consulta o registro **A** (IPv4). Você pode especificar diferentes tipos de registros adicionando-os ao final:

* **`dig exemplo.com`** — Consulta básica (retorna o registro A por padrão).
* **`dig exemplo.com A`** — Consulta o endereço **IPv4** do domínio.
* **`dig exemplo.com AAAA`** — Consulta o endereço **IPv6** do domínio.
* **`dig exemplo.com MX`** — Consulta os servidores de **e-mail** (Mail Exchange) do domínio.
* **`dig exemplo.com NS`** — Consulta os servidores de nomes (**Name Servers**) autoritativos.
* **`dig exemplo.com TXT`** — Consulta registros de texto (muito usados para SPF, DKIM, DMARC e validação de domínio).
* **`dig exemplo.com CNAME`** — Consulta o registro de apelido (**alias**) do domínio.
* **`dig exemplo.com SOA`** — Consulta as informações de início de autoridade (**Start of Authority**), incluindo serial e TTL.

---

## 2. Consultas em Servidores Específicos

Por padrão, o `dig` utiliza o servidor DNS configurado no seu sistema operacional (`/etc/resolv.conf` no Linux/macOS). Você pode forçar a consulta em um servidor específico usando o símbolo **`@`**:

* **`dig @8.8.8.8 exemplo.com`** — Consulta usando o DNS público do Google.
* **`dig @1.1.1.1 exemplo.com`** — Consulta usando o DNS público da Cloudflare.

---

## 3. Modificadores e Opções de Saída

Essas flags ajudam a filtrar, formatar ou rastrear a resposta do DNS de maneira mais eficiente:

* **`dig +short exemplo.com`** — Retorna apenas a resposta final limpa (por exemplo, apenas o endereço IP), excelente para scripts.
* **`dig +trace exemplo.com`** — Ativa o modo de rastreamento. Mostra todo o caminho da resolução de DNS (desde os servidores *root* globais até os servidores autoritativos do domínio).
* **`dig +noall +answer exemplo.com`** — Oculta os cabeçalhos longos e exibe apenas a seção de respostas (`ANSWER SECTION`), tornando a leitura muito mais limpa.
* **`dig +tcp exemplo.com`** — Força a consulta a ser realizada via protocolo **TCP** em vez do padrão UDP (útil para pacotes grandes ou testes de firewall).

---

## 4. Consulta Reversa (PTR)

* **`dig -x 8.8.8.8`** — Realiza uma busca reversa de DNS, descobrindo qual nome de host está associado a um determinado endereço IP.

---
