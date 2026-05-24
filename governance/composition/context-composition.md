# context-composition

Artifact ID: governance.context-composition
Kind: governance

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

`sizing` MAY ocorrer depois de intake quando a tarefa parecer grande demais para execucao direta ou quando houver pedido explicito de subagentes.

`sizing` MUST decidir entre `EXECUTE_DIRECT`, `DECOMPOSE_AND_DELEGATE` e `BLOCKED_FOR_DECOMPOSITION`.

`sizing` MUST NOT substituir intake, find, select, inject ou execute.

---

## Small Model Execution Mode

Modelos pequenos MUST executar apenas tarefas delimitadas, claras, baixo risco e com contexto explicitamente selecionado.

Modelos pequenos MUST NOT governar, redesenhar, aprovar ou expandir o sistema.

### Contexto inicial

Para modelos pequenos, a composicao inicial SHOULD conter no maximo:

- 1 prompt
- 1 rule principal
- 1 skill principal
- input da tarefa
- formato de saida esperado

`../../_memory/`, registry, remediation, evals e docs MUST NOT ser carregados por padrao nesse modo.

### Escalacao obrigatoria

Modelo pequeno MUST retornar `BLOCKED_OR_ESCALATE` quando a tarefa envolver:

- alteracao de `../../MANIFEST.md`
- alteracao em `../../governance/`
- alteracao em `../../docs/remediation/`
- alteracao em `../../evals/`
- criacao ou aprovacao de rule, skill, agent, prompt ou hook
- arquitetura
- mudanca estrutural
- decisao de taxonomia
- grow
- auditoria ampla
- conflito normativo
- seguranca operacional ou dados sensiveis
- acao destrutiva, irreversivel ou de amplo impacto

Formato obrigatorio:

```txt
BLOCKED_OR_ESCALATE
Reason:
Missing context:
Risk:
Suggested next artifact:
Suggested escalation:
```

`Suggested next artifact` SHOULD apontar no maximo um caminho inicial.

---

## Delegation Governance

Delegation Governance MAY ser acionada quando uma tarefa exceder execucao direta segura.

O orquestrador MUST manter responsabilidade por escopo, integracao e veredito final.

Subagentes MAY executar partes delimitadas, mas MUST NOT decidir governanca final, arquitetura final ou veredito final.

### Saidas oficiais de sizing

```txt
EXECUTE_DIRECT
DECOMPOSE_AND_DELEGATE
BLOCKED_FOR_DECOMPOSITION
```

### Contexto para delegacao

O contexto compartilhado para subtarefas SHOULD ser menor que o contexto total da tarefa.

Cada subtarefa delegada MUST declarar:

- objetivo
- escopo permitido
- arquivos permitidos
- arquivos proibidos
- entrada obrigatoria
- saida esperada
- criterio de aceite
- limites

Se a subtarefa nao puder ser descrita nesses termos, a delegacao MUST NOT ocorrer.

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
- tamanho da tarefa e necessidade de delegacao antes de `find`
- divida de contexto, redundancia, custo alto ou local incorreto de artefatos
- higiene mecanica do repositorio, referencias quebradas ou registros basicos ausentes
- neutralidade, anti-bajulacao e higiene de engajamento em respostas finais
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

### 0.1. Sizing antes de delegacao

`../../prompts/hooks/size-task-for-delegation.md` MAY ser usado depois de intake quando a tarefa parecer ampla, longa, multi-dominio ou quando o usuario pedir subagentes.

O sizing MUST terminar em uma das saidas:

- `EXECUTE_DIRECT`
- `DECOMPOSE_AND_DELEGATE`
- `BLOCKED_FOR_DECOMPOSITION`

Somente `DECOMPOSE_AND_DELEGATE` autoriza decomposicao e delegacao.

`EXECUTE_DIRECT` segue para `find -> select -> inject -> execute`.

`BLOCKED_FOR_DECOMPOSITION` exige esclarecimento, decisao ou reducao de escopo antes de continuar.

Sizing MUST NOT carregar `../../docs/`, `../../evals/`, registry ou `_memory/` por habito.

### 0.2. Context Debt Audit sob demanda

`../../prompts/hooks/validate-context-debt.md` MAY ser usado quando uma mudanca ou artefato parecer redundante, caro, mal localizado ou com responsabilidade misturada.

Context Debt Audit MUST terminar em uma das saidas:

- `KEEP`
- `TRIM`
- `MERGE`
- `MOVE`
- `SPLIT`
- `DEPRECATE`

Context Debt Audit MUST NOT ser acionado por padrao para typo, mudanca local pequena ou tarefa com criterio de aceite local.

Context Debt Audit MUST NOT executar remocao, merge, move ou split sem etapa posterior de implementacao e validacao.

### 0.3. Hygiene Governance sob demanda

`../../prompts/hooks/validate-repository-hygiene.md` MAY ser usado quando houver suspeita de garbage mecanico, referencia quebrada ou registro basico ausente.

Hygiene Governance MUST terminar em uma das saidas:

- `PASS`
- `FAIL_GARBAGE`
- `FAIL_BROKEN_REFERENCE`
- `FAIL_MISSING_REGISTRATION`
- `ESCALATE_CONTEXT_DEBT`
- `ESCALATE_LIFECYCLE`

Hygiene Governance MUST NOT apagar, mover, fundir, dividir ou depreciar artefatos.

Hygiene Governance MUST escalate quando a decisao depender de valor semantico, legado, depreciacao ou remocao.

### 0.4. Neutrality Governance sob demanda

`../../prompts/hooks/validate-neutrality-and-engagement.md` MAY ser usado antes de concluir resposta final ou artefato textual quando houver risco de bajulacao, concordancia indevida, falsa seguranca ou engajamento artificial.

Neutrality Governance MUST terminar em uma das saidas:

- `PASS`
- `TRIM_ENGAGEMENT`
- `REMOVE_SYCOPHANCY`
- `REWRITE_NEUTRAL`
- `BLOCK_MISLEADING_AGREEMENT`

Neutrality Governance MUST NOT criar persona, remover cordialidade minima ou bloquear pergunta necessaria para desambiguar.

### 1. Índice raiz para discovery inicial
`../../INDEX.md` MAY ser consultado no início de uma tarefa quando o agente ainda não souber qual roteador usar.

`../../INDEX.md` MUST ser descartado depois que o ponto de partida específico for escolhido.

`../../INDEX.md` MUST NOT substituir `../../MANIFEST.md`, roteadores locais, rules, skills, agents ou prompts.

### 2. Base padrão
`governance/` é a base padrão do ecossistema.

### 3. Relevância antes de injeção
Nenhum artefato SHOULD ser injetado sem relevância clara para a tarefa.

### 4. Governed Memory sob demanda

`../../_memory/` MAY ser considerada durante `find` quando a tarefa precisar de contexto pequeno, estavel e rastreavel de execucoes anteriores.

`../../_memory/` MUST NOT ser carregada antes de intake.

`../../_memory/` MUST NOT ser carregada por padrao.

`../../_memory/` MUST perder para qualquer fonte primaria aplicavel.

`../../_memory/` MUST ser descartada quando a fonte primaria especifica for carregada e suficiente.

### 5. Especialização sob demanda
`skills/` SHOULD ser carregado apenas quando a tarefa exigir capacidade especializada.

### 6. Regras por tipo de output ou intake
`rules/` SHOULD ser selecionado conforme o tipo de saída esperada.

`../../rules/quality/user-input-quality.md` SHOULD ser selecionado quando o intake precisar validar entrada humana.

### 7. Prompts como entrada
`prompts/` SHOULD iniciar a composição, e não substituir as fontes primárias das demais áreas.

### 8. Dependências explícitas
Prompts e agents MUST declarar quais tipos de artefatos precisam consumir.

Skills MUST declarar quais rules ou governance afetam seu uso.

Rules MUST declarar escopo e condição de aplicação.

### 9. Documentação humana fora da composição padrão
`../../docs/` MUST NOT ser injetado por padrão.

`../../docs/` MAY ser consultado apenas quando a tarefa for explicitamente sobre documentação humana, integração ou orientação operacional.

`../../LICENSE` MUST NOT ser tratado como contexto operacional.

### 10. Validação fora da composição padrão
`../../evals/` MUST NOT ser injetado por padrão.

`../../evals/` MAY ser consultado apenas quando a tarefa for explicitamente sobre validação, regressão, auditoria ou critério de aceite.

### 11. Checkpoints obrigatórios por risco
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
- modelos pequenos MUST NOT carregar governanca ampla antes de executar tarefa delimitada
- delegacao MUST NOT ser usada para tarefa simples
- subagentes MUST NOT receber contexto maior que o necessario para sua subtarefa
- Context Debt Audit MUST NOT ser carregado por padrao
- Hygiene Governance MUST NOT ser carregada por padrao
- Hygiene Governance MUST NOT decidir valor semantico nem apagar legado
- Neutrality Governance MUST NOT ser carregada por padrao
- respostas finais MUST NOT usar bajulacao, concordancia performatica ou engajamento artificial
- prompts MUST NOT embutir integralmente governança, regras ou skills
- agents MUST referenciar dependências em vez de embuti-las
- rules MUST NOT virar tutoriais operacionais
- skills MUST NOT virar normas obrigatórias
- documentação humana em `../../docs/` MUST NOT entrar na composição padrão
- validações em `../../evals/` MUST NOT entrar na composição padrão
- governed memory em `../../_memory/` MUST NOT entrar na composição padrão

---

## Critério de injeção aceitável

Uma composição de contexto é aceitável quando:

- cada artefato carregado tem motivo explícito
- cada dependência crítica está declarada por caminho
- nenhum artefato é carregado apenas por hábito
- modelos pequenos recebem contexto delimitado ou retornam `BLOCKED_OR_ESCALATE`
- tarefas grandes passam por sizing antes de delegacao
- subagentes recebem subtarefas verificaveis e o veredito permanece com o orquestrador
- auditoria de divida de contexto e selecionada apenas sob demanda e nao executa reestruturacao automaticamente
- higiene mecanica e selecionada apenas sob demanda e escala julgamento semantico para Context Debt ou Lifecycle
- neutralidade e validada sob demanda quando houver risco de bajulacao, falsa concordancia ou CTA artificial
- pedidos humanos ambíguos ou arriscados passam por intake antes de `find`
- a ordem `prompt -> governance -> agent -> rules -> skills` é preservada
- hooks são acionados apenas como checkpoints relevantes
- `../../docs/`, `../../evals/` e `../../LICENSE` ficam fora da composição padrão
- `../../INDEX.md` não permanece no contexto depois da seleção do roteador específico
- `../../_memory/` é selecionada apenas sob demanda, com motivo explícito e sem substituir fonte primária

---

## Limites

Este arquivo define composição de contexto.

Este arquivo não substitui:

- princípios fundacionais
- padrão de autoria
- lifecycle
- padrão de qualidade
