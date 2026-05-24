# delegation-boundaries

## Tipo do artefato

rule

## Finalidade

Definir limites normativos para decomposicao, delegacao e uso de subagentes.

Esta rule impede que delegacao vire terceirizacao de responsabilidade ou expansao descontrolada de escopo.

---

## Quando usar

Use esta rule quando:

- a tarefa parecer grande demais para execucao direta
- houver proposta de uso de subagentes
- a tarefa envolver muitos arquivos, dominios ou etapas
- a execucao precisar ser quebrada em subtarefas verificaveis
- o orquestrador precisar decidir entre executar, decompor ou bloquear

---

## Quando nao usar

Nao use esta rule como fonte primaria para:

- composicao geral de contexto
- qualidade da entrada humana
- prompt de sizing
- procedimento operacional detalhado

Consulte, respectivamente:

- `../../governance/composition/context-composition.md`
- `../quality/user-input-quality.md`
- `../../prompts/hooks/size-task-for-delegation.md`
- `../../skills/orchestration/task-decomposition-orchestration.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../docs/remediation/delegation-governance-spec.md`

---

## Normas

### 1. Sizing antes de delegar

O agente MUST avaliar se a tarefa cabe em execucao direta antes de delegar.

Delegacao por reflexo MUST NOT ocorrer.

### 2. Criterio para tarefa grande

Uma tarefa SHOULD ser tratada como grande quando atender dois ou mais criterios:

- toca mais de um dominio operacional
- altera mais de tres grupos de artefatos
- mistura implementacao, documentacao, evals e governanca
- exige revisao independente
- envolve risco P0/P1
- pode exceder a janela de contexto util
- exige auditoria coletiva

### 3. Tarefa simples permanece direta

Uma tarefa MUST permanecer direta quando:

- tem escopo pequeno
- tem criterio de aceite local
- altera um unico artefato ou grupo coeso de artefatos
- nao exige julgamento independente
- nao muda governanca central

### 4. Contrato obrigatorio de subtarefa

Toda subtarefa delegada MUST declarar:

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

Subtarefa sem contrato claro MUST NOT ser delegada.

### 5. Write sets disjuntos

Subagentes SHOULD ter conjuntos de arquivos disjuntos.

Quando sobreposicao for inevitavel, o orquestrador MUST declarar o conflito esperado e integrar manualmente.

### 6. Veredito nao delegavel

Subagente MUST NOT decidir veredito final.

O orquestrador MUST revisar, integrar e assumir a decisao final.

### 7. Governanca central exige orquestrador

Subagente MUST NOT alterar `../../MANIFEST.md`, `../../governance/`, registry, remediation ou evals sem autorizacao explicita do orquestrador.

### 8. Bloqueio quando nao houver decomposicao segura

Se a tarefa for grande mas nao puder ser quebrada com seguranca, a saida MUST ser:

```txt
BLOCKED_FOR_DECOMPOSITION
Reason:
Missing decision:
Risk:
Suggested clarification:
```

---

## Criterio de conformidade

Uma delegacao esta conforme quando:

- houve sizing antes da delegacao
- cada subtarefa tem contrato verificavel
- subagentes nao ampliaram escopo
- write sets foram isolados ou conflito foi declarado
- o orquestrador revisou os resultados
- o veredito final foi emitido pelo orquestrador

---

## Limites

Esta rule governa limites de delegacao.

Ela nao substitui:

- composicao de contexto em `../../governance/composition/context-composition.md`
- intake em `../quality/user-input-quality.md`
- procedimento de orquestracao em `../../skills/orchestration/task-decomposition-orchestration.md`
