# task-decomposition-orchestration

## Tipo do artefato

skill

## Finalidade

Definir o procedimento reutilizavel para quebrar tarefas grandes, delegar subtarefas e integrar resultados sob responsabilidade do orquestrador.

Esta skill operacionaliza Delegation Governance sem criar runtime multiagente nem burocracia para tarefas simples.

---

## Quando usar

Use esta skill quando:

- `../../prompts/hooks/size-task-for-delegation.md` retornar `DECOMPOSE_AND_DELEGATE`
- a tarefa exigir subagentes por escopo, revisao ou paralelismo
- houver muitas etapas independentes
- o orquestrador precisar manter veredito final
- a execucao direta aumentaria risco de contexto excessivo

---

## Quando nao usar

Nao use esta skill quando:

- a tarefa couber em execucao direta
- o intake ainda estiver pendente
- a decomposicao depender de decisao humana ausente
- a delegacao transferiria responsabilidade de governanca
- as subtarefas editariam os mesmos arquivos sem necessidade

Consulte, respectivamente:

- `../../prompts/hooks/validate-user-intent.md`
- `../../prompts/hooks/size-task-for-delegation.md`
- `../../rules/architecture/delegation-boundaries.md`

---

## Dependencias relacionadas

- `../../governance/composition/context-composition.md`
- `../../rules/architecture/delegation-boundaries.md`
- `../../prompts/hooks/size-task-for-delegation.md`

---

## Procedimento

### 1. Confirmar permissao de delegacao

Antes de delegar, confirme que:

- intake liberou a tarefa ou nao era necessario
- sizing retornou `DECOMPOSE_AND_DELEGATE`
- a tarefa pode ser quebrada com seguranca
- o orquestrador tem criterio de aceite final

### 2. Criar mapa de subtarefas

Cada subtarefa MUST ser pequena, verificavel e ter responsabilidade unica.

Use o contrato:

```txt
Subtask ID:
Objetivo:
Escopo permitido:
Arquivos permitidos:
Arquivos proibidos:
Entrada obrigatoria:
Saida esperada:
Criterio de aceite:
Limites:
```

### 3. Isolar write sets

Subtarefas de implementacao SHOULD ter arquivos permitidos disjuntos.

Se dois subagentes precisarem tocar o mesmo arquivo, o orquestrador SHOULD manter esse arquivo localmente e pedir aos subagentes apenas achados ou propostas.

### 4. Delegar somente partes

Subagentes podem:

- investigar
- implementar fatia definida
- revisar criterio especifico
- validar contrato local
- apontar risco

Subagentes nao podem:

- alterar escopo
- decidir arquitetura final
- aprovar governanca
- emitir veredito final
- substituir fonte primaria

### 5. Revisar outputs

Para cada retorno de subagente, o orquestrador MUST verificar:

- aderencia ao escopo
- arquivos tocados
- conflitos com outras subtarefas
- conformidade com rules e governance
- lacunas, riscos e premissas

### 6. Integrar

O orquestrador integra apenas resultados que:

- preservam a filosofia do repo
- reduzem contexto ou ambiguidade
- mantem responsabilidade unica
- nao duplicam fonte primaria
- passam no criterio de aceite da subtarefa

### 7. Validar

Antes do veredito, o orquestrador SHOULD executar validacao proporcional ao risco:

- leitura de contratos alterados
- busca por referencias quebradas
- eval manual quando comportamento muda
- `git diff --check` quando houver edicao local

### 8. Emitir veredito

O veredito final MUST ser do orquestrador.

Use:

```txt
ORCHESTRATOR VERDICT
Status: PASS | FAIL | CONDITIONAL
Scope:
Subtasks reviewed:
Evidence:
Residual risks:
Next action:
```

---

## Limites

Esta skill descreve decomposicao e orquestracao.

Ela nao substitui:

- rule de limites em `../../rules/architecture/delegation-boundaries.md`
- hook de sizing em `../../prompts/hooks/size-task-for-delegation.md`
- composicao de contexto em `../../governance/composition/context-composition.md`
- veredito humano quando producao critica exigir aprovacao externa
