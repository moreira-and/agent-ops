# plan-data-task

## Tipo do artefato

prompt

## Finalidade

Orientar o planejamento de uma tarefa antes da execução, com composição contextual controlada.

---

## Quando usar

Use este prompt quando precisar:

- decompor uma tarefa antes de executar
- decidir estratégia de abordagem
- explicitar dependências e contexto necessário
- reduzir improviso e ambiguidade

---

## Quando não usar

Não use este prompt quando o objetivo principal for:

- gerar a solução final
- revisar uma solução existente
- descobrir contexto do zero
- validar conformidade final

Consulte, nesses casos:

- `../generation/generate-data-solution.md`
- `../review/review-data-solution.md`
- `../discovery/discover-required-context.md`
- `../hooks/validate-context-and-output.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`

---

## Composição recomendada

### Base
- `../../governance/principles/core-principles.md`
- `../../governance/composition/context-composition.md`

### Apoio
Selecionar conforme a tarefa em:
- `../../agents/`
- `../../rules/`
- `../../skills/`

---

## Instrução operacional

Ao usar este prompt, o agente MUST:

1. explicitar o objetivo da tarefa
2. decompor a tarefa em etapas coerentes
3. identificar contexto obrigatório e contexto condicional
4. apontar qual agente deve ser usado
5. apontar quais rules e skills serão necessárias
6. explicitar riscos, lacunas e dependências
7. evitar iniciar execução sem contexto crítico mínimo

---

## Saída esperada

A saída MUST:

- apresentar plano claro e sequencial
- indicar contexto necessário por caminho
- diferenciar etapa de planejamento de etapa de execução
- reduzir ambiguidade antes da ação

---

## Limites

Este prompt planeja a execução.

Este prompt não executa a entrega final nem substitui prompts de geração, revisão ou validação.
