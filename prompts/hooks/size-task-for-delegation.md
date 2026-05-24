# size-task-for-delegation

## Tipo do artefato

hook prompt

## Status de injecao

condicional

## Finalidade

Avaliar se uma tarefa deve ser executada diretamente, decomposta para delegacao ou bloqueada por falta de decomposicao segura.

Este hook implementa o checkpoint operacional de Task Sizing dentro de Delegation Governance.

---

## Quando usar

Use este hook depois de intake e antes de `find` quando:

- a tarefa parecer grande demais para uma unica execucao
- o usuario pedir uso de subagentes ou long running
- houver muitos dominios, arquivos ou etapas
- a tarefa misturar implementacao, documentacao, evals e governanca
- houver risco de leitura indiscriminada por excesso de escopo
- o orquestrador precisar decidir entre executar e delegar

---

## Quando nao usar

Nao use este hook quando:

- a tarefa for claramente pequena e direta
- a decisao de intake ainda nao liberou a tarefa
- o pedido ainda precisar de esclarecimento basico
- outro checkpoint de seguranca operacional for o bloqueio principal

Consulte, nesses casos:

- `./validate-user-intent.md`
- `./validate-operational-safety.md`
- `../planning/plan-data-task.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../rules/architecture/delegation-boundaries.md`

---

## Artefatos relacionados

- `../../skills/orchestration/task-decomposition-orchestration.md`

---

## Instrucao operacional

Ao usar este hook, o agente MUST:

1. partir do pedido humano e da decisao de intake, se existir
2. avaliar tamanho, risco, dominios afetados e grupos de artefatos
3. decidir se a tarefa cabe em execucao direta
4. se nao couber, propor subtarefas pequenas e verificaveis
5. declarar contexto compartilhado minimo
6. declarar validacao obrigatoria do orquestrador
7. bloquear quando a decomposicao depender de decisao ausente
8. nao executar a tarefa final

---

## Saidas oficiais

Use exatamente uma:

- `EXECUTE_DIRECT`
- `DECOMPOSE_AND_DELEGATE`
- `BLOCKED_FOR_DECOMPOSITION`

---

## Regras de decisao

Retorne `EXECUTE_DIRECT` quando:

- a tarefa for pequena
- o contexto necessario for limitado
- nao houver necessidade de revisao independente
- o criterio de aceite for local

Retorne `DECOMPOSE_AND_DELEGATE` quando:

- a tarefa for grande
- puder ser quebrada em subtarefas independentes
- cada subtarefa tiver entrada e saida verificaveis
- o orquestrador puder revisar e integrar

Retorne `BLOCKED_FOR_DECOMPOSITION` quando:

- a tarefa for grande
- faltar decisao, escopo, prioridade ou criterio de aceite para quebrar com seguranca
- a delegacao criaria conflito de responsabilidade
- o risco exigir esclarecimento antes de seguir

---

## Saida esperada

```txt
TASK SIZING
Status: EXECUTE_DIRECT | DECOMPOSE_AND_DELEGATE | BLOCKED_FOR_DECOMPOSITION
Reason:
Size: small | medium | large
Risk: low | medium | high
Domains affected:
Context needed:
Subtasks:
Shared context:
Orchestrator validation:
Missing decision:
Next allowed action:
```

---

## Limites

Este hook dimensiona a tarefa.

Ele nao executa, nao delega de fato, nao substitui intake e nao decide veredito final.
