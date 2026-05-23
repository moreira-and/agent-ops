# validate-context-and-output

## Tipo do artefato

hook prompt

## Finalidade

Executar um checkpoint de validação sobre contexto carregado e/ou saída produzida.

---

## Quando usar

Use este prompt quando precisar:

- validar se o contexto selecionado faz sentido
- revisar aderência a regras carregadas
- verificar conformidade antes da conclusão
- identificar lacunas, conflito ou excesso de contexto

---

## Quando não usar

Não use este prompt quando o objetivo principal for:

- descobrir contexto do zero
- planejar a tarefa
- gerar a solução inicial
- realizar revisão técnica ampla sem foco em conformidade

Consulte, nesses casos:

- `../discovery/discover-required-context.md`
- `../planning/plan-data-task.md`
- `../generation/generate-data-solution.md`
- `../review/review-data-solution.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../governance/quality/artifact-quality-standard.md`
- `../../rules/generation/operational-safety-guardrails.md`

---

## Composição recomendada

### Base
- `../../governance/composition/context-composition.md`
- `../../governance/quality/artifact-quality-standard.md`

### Regras
Selecionar conforme o caso em:
- `../../rules/`
- especialmente `../../rules/quality/`
- especialmente `../../rules/generation/`

### Skills de apoio
Selecionar se necessário:
- `../../skills/quality/`
- `../../skills/review/`

---

## Instrução operacional

Ao usar este prompt, o agente SHOULD:

1. listar o contexto carregado
2. validar se cada artefato carregado é relevante
3. verificar lacunas críticas de contexto
4. verificar excesso de contexto carregado
5. verificar se `../../docs/`, `../../evals/` ou `../../LICENSE` foram carregados indevidamente
6. verificar aderência da saída às regras aplicáveis
7. verificar se risco operacional exige `./validate-operational-safety.md`
8. explicitar conflitos, não conformidades e incertezas
9. recomendar ajuste antes da conclusão, quando necessário

---

## Saída esperada

A saída SHOULD:

- apontar conformidades e não conformidades
- indicar contexto ausente ou excessivo
- indicar uso indevido de documentação humana, evals ou metadados, quando houver
- diferenciar problema estrutural de problema de output
- apoiar correção antes da etapa final

---

## Limites

Este hook valida contexto carregado e saída produzida.

Este hook não substitui revisão técnica ampla nem prompts de geração, discovery ou planejamento.
