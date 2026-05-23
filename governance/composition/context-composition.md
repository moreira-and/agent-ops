# context-composition

## Tipo do artefato

governance

## Finalidade

Definir o padrão oficial de descoberta, seleção, composição e injeção de contexto no `agent-ops`.

---

## Quando usar

Use este arquivo quando precisar:

- compor contexto para execução
- decidir ordem de carregamento
- reduzir contexto desnecessário
- distinguir conteúdo base de conteúdo condicional
- aplicar checkpoints de validação

---

## Quando não usar

Não use este arquivo como fonte primária para:

- padrão de autoria de Markdown
- lifecycle de artefatos
- regra técnica de output
- skill operacional

Consulte, respectivamente:

- `../authoring/markdown-authoring-standard.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../../rules/`
- `../../skills/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../principles/core-principles.md`

---

## Modelo operacional

O `agent-ops` MUST operar no modelo:

**find -> select -> inject**

### find
Descobrir quais artefatos existem e quais são relevantes.

### select
Escolher apenas os artefatos necessários para a tarefa.

### inject
Carregar apenas o contexto mínimo necessário para execução confiável.

Esse modelo é a forma oficial de injeção de dependências em Markdown.

O agente MUST montar contexto por arquivos declarados e selecionados, não por leitura indiscriminada do repositório.

---

## Ordem oficial de composição

A ordem oficial é:

```txt
prompt -> governance -> agent -> rules -> skills
```

### Interpretação

#### 1. prompt
Define o ponto de entrada da tarefa.

#### 2. governance
Carrega a base estrutural padrão.

#### 3. agent
Define o perfil executor.

#### 4. rules
Define restrições de output.

#### 5. skills
Adiciona conhecimento operacional especializado.

---

## Uso de checkpoints

`../../prompts/hooks/` MAY ser acionado em pontos específicos do fluxo para validar:

- aderência a `governance/`
- aderência a `rules/`
- conformidade antes da conclusão

`../../prompts/hooks/` NÃO integra a base obrigatória padrão.

---

## Regras de seleção

### 1. Base padrão
`governance/` é a base padrão do ecossistema.

### 2. Relevância antes de injeção
Nenhum artefato SHOULD ser injetado sem relevância clara para a tarefa.

### 3. Especialização sob demanda
`skills/` SHOULD ser carregado apenas quando a tarefa exigir capacidade especializada.

### 4. Regras por tipo de output
`rules/` SHOULD ser selecionado conforme o tipo de saída esperada.

### 5. Prompts como entrada
`prompts/` SHOULD iniciar a composição, e não substituir as fontes primárias das demais áreas.

### 6. Dependências explícitas
Prompts e agents MUST declarar quais tipos de artefatos precisam consumir.

Skills MUST declarar quais rules ou governance afetam seu uso.

Rules MUST declarar escopo e condição de aplicação.

### 7. Documentação humana fora da composição padrão
`../../docs/` MUST NOT ser injetado por padrão.

`../../docs/` MAY ser consultado apenas quando a tarefa for explicitamente sobre documentação humana, integração ou orientação operacional.

`../../LICENSE` MUST NOT ser tratado como contexto operacional.

### 8. Validação fora da composição padrão
`../../evals/` MUST NOT ser injetado por padrão.

`../../evals/` MAY ser consultado apenas quando a tarefa for explicitamente sobre validação, regressão, auditoria ou critério de aceite.

### 9. Checkpoints obrigatórios por risco
Hooks continuam condicionais para tarefas comuns.

Um checkpoint de validação MUST ser acionado quando a tarefa envolver:

- proposta de grow ou alteração estrutural do `agent-ops`
- operação destrutiva, irreversível ou de amplo impacto
- dados sensíveis, credenciais ou segredos
- saída que declare conformidade, bloqueio ou aprovação
- conflito entre artefatos normativos

---

## Regras de contenção de ruído

- contexto opcional MUST NOT ser carregado por hábito
- múltiplas skills MUST NOT ser carregadas sem necessidade
- prompts MUST NOT embutir integralmente governança, regras ou skills
- agents MUST referenciar dependências em vez de embuti-las
- rules MUST NOT virar tutoriais operacionais
- skills MUST NOT virar normas obrigatórias
- documentação humana em `../../docs/` MUST NOT entrar na composição padrão
- validações em `../../evals/` MUST NOT entrar na composição padrão

---

## Critério de injeção aceitável

Uma composição de contexto é aceitável quando:

- cada artefato carregado tem motivo explícito
- cada dependência crítica está declarada por caminho
- nenhum artefato é carregado apenas por hábito
- a ordem `prompt -> governance -> agent -> rules -> skills` é preservada
- hooks são acionados apenas como checkpoints relevantes
- `../../docs/`, `../../evals/` e `../../LICENSE` ficam fora da composição padrão

---

## Limites

Este arquivo define composição de contexto.

Este arquivo não substitui:

- princípios fundacionais
- padrão de autoria
- lifecycle
- padrão de qualidade
