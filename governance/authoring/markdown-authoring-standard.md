# markdown-authoring-standard

## Tipo do artefato

governance

## Finalidade

Definir o padrão de escrita dos arquivos `.md` do `agent-ops`.

---

## Quando usar

Use este arquivo quando precisar:

- criar novo arquivo
- revisar a estrutura de um arquivo
- padronizar linguagem e seções
- melhorar legibilidade e interpretabilidade por humanos e agentes

---

## Quando não usar

Não use este arquivo como fonte primária para:

- composição de contexto
- lifecycle de artefatos
- critério de qualidade final
- regra técnica de output

Consulte, respectivamente:

- `../composition/context-composition.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../quality/artifact-quality-standard.md`
- `../../rules/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../principles/core-principles.md`

---

## Regras de escrita

### 1. Clareza de propósito
Todo arquivo SHOULD declarar explicitamente:

- o que é
- para que serve
- quando usar
- quando não usar

---

### 2. Identificação do tipo
Todo arquivo SHOULD indicar seu tipo de artefato quando fizer sentido.

Exemplos:
- governance
- agent
- rule
- skill
- prompt

---

### 3. Escopo e limites
Todo arquivo SHOULD declarar:

- o que cobre
- o que não cobre
- para onde encaminhar temas fora do seu escopo

---

### 4. Responsabilidade única
Todo arquivo MUST possuir uma única responsabilidade contextual.

O arquivo SHOULD ser dividido quando misturar:

- prompt + rule
- agent + skill
- governance + rule de output
- documentação humana + instrução injetável
- histórico de execução + norma reutilizável

---

### 5. Dependências por caminho
Toda dependência MUST ser referenciada por caminho.

---

### 6. Baixo acoplamento
Um arquivo SHOULD depender de contratos e caminhos explícitos, não de memória externa ou leitura implícita.

Arquivos de alto nível SHOULD referenciar artefatos especializados em vez de copiar seu conteúdo.

---

### 7. Estruturação por seções
Arquivos SHOULD ser organizados em seções curtas e previsíveis.

Estruturas muito longas ou pouco navegáveis SHOULD ser evitadas.

---

### 8. Linguagem normativa
Arquivos normativos SHOULD usar linguagem como:

- MUST
- MUST NOT
- SHOULD
- SHOULD NOT
- MAY

---

### 9. Baixa ambiguidade
O texto SHOULD evitar:

- termos vagos
- sobreposição implícita
- referências não rastreáveis
- recomendações sem contexto

---

### 10. Legibilidade para LLM
O texto SHOULD favorecer:

- frases diretas
- subtítulos claros
- fronteiras explícitas
- instruções objetivas
- baixa inferência implícita

---

### 11. Não duplicação
Um arquivo MUST NOT copiar extensivamente conteúdo de sua fonte primária externa.

Quando necessário, ele SHOULD resumir minimamente e referenciar a fonte por caminho.

---

## Estrutura mínima recomendada

Sempre que aplicável, um arquivo SHOULD conter:

- título
- tipo do artefato
- status de injeção
- finalidade
- quando usar
- quando não usar
- dependências relacionadas
- artefatos relacionados
- precedência
- limites
- instrução operacional
- saídas esperadas

Essas seções SHOULD ser adicionadas apenas quando reduzirem inferência ou melhorarem seleção modular.

---

## Limites

Este arquivo define padrão de autoria.

Este arquivo não define:

- ordem de composição
- política de lifecycle
- padrão de qualidade
