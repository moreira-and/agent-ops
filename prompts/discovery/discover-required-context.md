# discover-required-context

## Tipo do artefato

prompt

## Finalidade

Orientar a descoberta do contexto necessário antes da execução de uma tarefa.

---

## Quando usar

Use este prompt quando precisar:

- decidir quais artefatos carregar
- evitar injeção excessiva
- identificar o agente apropriado
- selecionar regras e skills por relevância

---

## Quando não usar

Não use este prompt quando o objetivo principal for:

- gerar a solução final
- revisar um artefato existente
- executar checkpoint de validação
- detalhar plano completo de execução

Consulte, nesses casos:

- `../generation/generate-data-solution.md`
- `../review/review-data-solution.md`
- `../hooks/validate-context-and-output.md`
- `../planning/plan-data-task.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../README.md`
- `../../governance/composition/context-composition.md`

---

## Composição recomendada

### Base
- `../../MANIFEST.md`
- `../../README.md`

### Apoio
- `../../agents/README.md`
- `../../rules/README.md`
- `../../skills/README.md`
- `../../prompts/README.md`

---

## Instrução operacional

Ao usar este prompt, o agente MUST:

1. identificar o objetivo da tarefa
2. identificar se a tarefa é de geração, revisão, planejamento ou discovery
3. selecionar o perfil de agente mais adequado
4. selecionar apenas as regras necessárias ao tipo de saída
5. selecionar apenas as skills necessárias à execução
6. excluir `../../docs/` e `../../LICENSE` da composição padrão
7. explicitar quais artefatos serão carregados e por quê
8. apontar lacunas de contexto antes de avançar

---

## Saída esperada

A saída MUST:

- listar contexto recomendado por caminho
- justificar a seleção
- diferenciar base padrão de contexto condicional
- indicar que `../../docs/`, `../../evals/` e `../../LICENSE` não foram selecionados, salvo tarefa explicitamente documental, de validação ou de metadado
- reduzir ruído de injeção
- preparar a próxima etapa com clareza

---

## Limites

Este prompt descobre contexto necessário.

Este prompt não executa geração, revisão final ou validação formal.
