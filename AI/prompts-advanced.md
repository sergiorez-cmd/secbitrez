# Técnicas de Prompt:

Um prompt é o texto ou consulta de entrada fornecido a um modelo de IA, como um grande modelo de linguagem, para gerar uma resposta. Ele serve como o mecanismo principal para orientar o comportamento do modelo, definindo a tarefa e configurando o contexto para a interação. O design de um prompt afeta significativamente a qualidade e a relevância da saída, tornando essencial a escolha do tipo certo de prompt para tarefas específicas.

Para obter os melhores resultados dos modelos de IA, é essencial entender as várias maneiras pelas quais os prompts podem ser estruturados para se adequar a diferentes tarefas e objetivos. Existem três maneiras principais de estruturar o prompt: instruções diretas, instruções abertas e instruções específicas da tarefa.

As instruções diretas são comandos claros e específicos que dizem à IA exatamente o que fazer. Esses prompts são ideais para tarefas simples em que o usuário tem uma expectativa clara da saída. Os prompts diretos dependem da capacidade do modelo de analisar instruções explícitas e gerar respostas que se alinham rigorosamente com o comando. Quanto mais detalhada for a instrução, maior a probabilidade de a saída atender às expectativas.

**Instrução Direta:**
```text
Escreva uma resumo sobre cibersegurança.
```

**Instrução Aberta:**
```text
Fale-me sobre o hacking ético.
```

**Instrução Específica:**
```text
Explique o que este comando faz "nmap scanme.nmap.org"
```

**Prompt normal:**
```text
Explique o conceito de hacking ético, suas principais funções, e seu valor no mercado de um modo acessível para um público geral.
```

**Prompt Zero-Shot:**

Pedir ao modelo que execute uma tarefa sem fornecer quaisquer exemplos ou orientações prévias.
```text
Explique o conceito de hacking ético, suas principais funções, e seu valor no mercado em termos simples.
```

**Prompt Few-Shot:**

Inclui um pequeno número de exemplos dentro do prompt para demonstrar a tarefa ao modelo. Essa abordagem ajuda o modelo a entender melhor o contexto e a saída esperada.
```text
Tópico: Cibersegurança

Explicação: A cibersegurança (ou segurança cibernética) é o conjunto de práticas, tecnologias e processos projetados para proteger computadores, servidores, redes, dispositivos móveis e dados contra ataques, danos ou acessos não autorizados.

Tópico: Vulnerabilidades

Explicação: Vulnerabilidade na cibersegurança é uma fraqueza, falha ou brecha em um sistema, software, rede, processo ou comportamento humano que pode ser explorada por agentes maliciosos para comprometer dados ou ativos.
```

**Prompt de cadeia de pensamentos (CoT):**

Incentiva o modelo a raciocinar sobre um problema passo a passo, dividindo-o em componentes menores para chegar a uma conclusão lógica.
```text
Passo 1: Defina o que é cibersegurança.

Passo 2: Explique qual sua importancia para a TI.

Passo 3: Descreva seus beneficios para as empresas.

Agora, siga esses passos para explicar o hacking ético.
```

**Metaprompt:**

Envolve pedir ao modelo que gere ou refine seus próprios prompts para executar melhor a tarefa. Essa técnica pode melhorar a qualidade da saída ao aproveitar a capacidade de autodirecionamento do modelo.
```text
Crie um prompt que ajude a explicar o conceito de hacking ético, suas principais funções, e seu valor no mercado em termos simples.
```

**Prompt de Autoconsistência:**

Utiliza várias gerações independentes do modelo para identificar a resposta mais coerente ou precisa. É particularmente útil para tarefas que exigem raciocínio ou interpretação.
```text
Providencie três diferentes explicações para o conceito de hacking ético, suas principais funções e seu valor no mercado. Depois identifique a explicação mais clara e coerente.
```

**Prompt de conhecimento:**

Envolve pedir ao modelo que gere conhecimento prévio antes de lidar com a tarefa principal, aprimorando sua capacidade de produzir respostas informadas e precisas.
```text
Antes de explicar o que é hacking ético, primeiro liste os principios técnicos relacionados. Feito isso, use os principios para explicar o conceito, suas principais funções e seu valor no mercado.
```

**Encadeamento de prompts:**

Envolve a vinculação de vários prompts, onde a saída de um prompt serve como entrada para o próximo. Essa técnica é ideal para processos multietapas.

1° prompt
```text
O que é hacking ético? Forneça uma breve definição.
```
2° prompt baseado na resposta anterior:
```text
Quais são as principais funçoes do hacking ético?
```
3° prompt com base na resposta anterior: 
```text
Quais os benefícios do hacking ético para uma empresa e sua infraestrutura de TI?
```

**Prompt de árvore de pensamentos:**

Incentiva o modelo a explorar vários ramos de raciocínio ou ideias antes de chegar a um resultado final.
```text
Liste três possíveis modos para explicar o hacking ético para um público geral. Para cada método, descreva suas vantagens e desvantagens. Então escolha a melhor explicação e desenvolva-a.
```

**Geração aumentada de recuperação (RAG):**

Combina a recuperação de informações externas com a IA generativa para produzir respostas com base em conhecimentos atualizados ou específicos do domínio.
```text
Utilize como base este link da IBM https://www.ibm.com/think/topics/ethical-hacking, explique suas principais funções, e seu valor no mercado em termos simples.
```

**Engenheiro de prompts automático:**

Envolve o uso da própria IA para gerar e otimizar prompts para tarefas específicas, automatizando o processo de elaboração de instruções eficazes.
```text
Gere um prompt que ajude a explicar o hacking ético, suas principais funções, e seu valor no mercado. Em seguida, utilize o prompt gerado para fornecer a explicação.
```

**Prompt ativo:**

Ajusta dinamicamente o prompt com base em resultados intermediários do modelo, refinando a entrada para obter melhores resultados.

1° prompt
```text
Explique o que é hacking ético, suas principais funções, e seu valor no mercado em termos simples.
```
2° Prompt de acompanhamento
```text
E procure por mais detalhes sobre os benefícios, focado no ambiente de TI.
```

**Prompt de estímulo direcional(DSP):**

Utiliza pistas direcionais para levar o modelo em direção a um tipo específico de resposta ou perspectiva.
```text
Explique o conceito de cibersegurança sob a perspectiva de um especialista, enfatizando a necessidade no ambiente de TI de uma empresa.
```

**Prompt ReAct:**

O ReAct combina prompts de raciocínio e ação, incentivando o modelo a pensar criticamente e a agir com base em seu raciocínio.

Adicione um documento para ser analisado pela IA
```text
Analise os seguintes dados deste relatório e identifique as principais tendências. Com base em sua análise, explique o conceito de ameaças cibernéticas para IA, suas causas e seus efeitos.
```

**Cadeia de pensamentos multimodal (CoT multimodal):**

Integra o raciocínio da cadeia de pensamentos em várias modalidades, como texto, imagens ou áudio.
```text
Analise este infográfico de tendências de ameaças cibernéticas, então explique as ameaças a cibersegurança, suas causas, e seus efeitos passo a passo.
```

