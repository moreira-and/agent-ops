# context-composition

## Tipo do artefato

governance

## Finalidade

Definir o padrão oficial de intake, descoberta, seleção, composição, injeção e execução de contexto no `agent-ops`.

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

**intake -> find -> select -> inject -> execute**

### intake
Validar a entrada humana antes de descobrir contexto.

`intake` MUST classificar intenção, ambiguidade, risco, necessidade de aprovação e critério mínimo de sucesso quando o pedido não estiver claramente seguro.

### find
Descobrir quais artefatos existem e quais são relevantes.

### select
Escolher apenas os artefatos necessários para a tarefa.

### inject
Carregar apenas o contexto mínimo necessário para execução confiável.

### execute
Executar a tarefa dentro dos limites definidos pelo intake e pelos artefatos injetados.

Esse modelo é a forma oficial de injeção de dependências em Markdown.

O agente MUST montar contexto por arquivos declarados e selecionados, não por leitura indiscriminada do repositório.

`intake` MUST NOT ser usado como justificativa para carregar mais contexto antes de `find`.

---

## Ordem oficial de composição

A ordem oficial é:

```txt
prompt -> governance -> agent -> rules -> skills
```

### Interpretação

Esta ordem se aplica depois que a tarefa estiver liberada para `find`.

#### 1. prompt
Define o ponto de entrada da tarefa.

#### 2. governance
Carrega a base estrutural padrão.

#### 3. agent
Define o perfil executor.

#### 4. rules
Define restrições de output e regras de intake quando aplicável.

#### 5. skills
Adiciona conhecimento operacional especializado.

---

## Uso de checkpoints

`../../prompts/hooks/` MAY ser acionado em pontos específicos do fluxo para validar:

- intenção, ambiguidade e risco do pedido humano antes de `find`
- aderência a `governance/`
- aderência a `rules/`
- conformidade antes da conclusão

`../../prompts/hooks/` NÃO integra a base obrigatória padrão.

---

## Regras de seleção

### 0. Intake antes do discovery

`../../prompts/hooks/validate-user-intent.md` MAY ser usado antes de `find` quando o pedido humano estiver vago, amplo, contraditório, arriscado ou sem critério mínimo de sucesso.

O intake MUST terminar em uma das saídas:

- `READY_TO_FIND`
- `NEEDS_CLARIFICATION`
- `NEEDS_APPROVAL`
- `REFUSE_OR_REDIRECT`

Somente `READY_TO_FIND` libera o fluxo normal de `find -> select -> inject -> execute`.

Intake MUST NOT carregar `../../docs/`, `../../evals/` ou contexto especializado por hábito.

### 1. Índice raiz para discovery inicial
`../../INDEX.md` MAY ser consultado no início de uma tarefa quando o agente ainda não souber qual roteador usar.

`../../INDEX.md` MUST ser descartado depois que o ponto de partida específico for escolhido.

`../../INDEX.md` MUST NOT substituir `../../MANIFEST.md`, roteadores locais, rules, skills, agents ou prompts.

### 2. Base padrão
`governance/` é a base padrão do ecossistema.

### 3. Relevância antes de injeção
Nenhum artefato SHOULD ser injetado sem relevância clara para a tarefa.

### 4. Especialização sob demanda
`skills/` SHOULD ser carregado apenas quando a tarefa exigir capacidade especializada.

### 5. Regras por tipo de output ou intake
`rules/` SHOULD ser selecionado conforme o tipo de saída esperada.

`../../rules/quality/user-input-quality.md` SHOULD ser selecionado quando o intake precisar validar entrada humana.

### 6. Prompts como entrada
`prompts/` SHOULD iniciar a composição, e não substituir as fontes primárias das demais áreas.

### 7. Dependências explícitas
Prompts e agents MUST declarar quais tipos de artefatos precisam consumir.

Skills MUST declarar quais rules ou governance afetam seu uso.

Rules MUST declarar escopo e condição de aplicação.

### 8. Documentação humana fora da composição padrão
`../../docs/` MUST NOT ser injetado por padrão.

`../../docs/` MAY ser consultado apenas quando a tarefa for explicitamente sobre documentação humana, integração ou orientação operacional.

`../../LICENSE` MUST NOT ser tratado como contexto operacional.

### 9. Validação fora da composição padrão
`../../evals/` MUST NOT ser injetado por padrão.

`../../evals/` MAY ser consultado apenas quando a tarefa for explicitamente sobre validação, regressão, auditoria ou critério de aceite.

### 10. Checkpoints obrigatórios por risco
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
- pedidos humanos ambíguos ou arriscados passam por intake antes de `find`
- a ordem `prompt -> governance -> agent -> rules -> skills` é preservada
- hooks são acionados apenas como checkpoints relevantes
- `../../docs/`, `../../evals/` e `../../LICENSE` ficam fora da composição padrão
- `../../INDEX.md` não permanece no contexto depois da seleção do roteador específico

---

## Limites

Este arquivo define composição de contexto.

Este arquivo não substitui:

- princípios fundacionais
- padrão de autoria
- lifecycle
- padrão de qualidade
