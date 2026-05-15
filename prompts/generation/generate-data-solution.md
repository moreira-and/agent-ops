# generate-data-solution

## Tipo do artefato

prompt

## Finalidade

Iniciar a geração de uma solução ou artefato de engenharia de dados com composição contextual controlada.

---

## Quando usar

Use este prompt quando precisar:

- gerar uma solução nova
- estruturar uma implementação
- produzir um artefato técnico com base em contexto selecionado
- conduzir geração com aderência ao `agent-ops`

---

## Quando não usar

Não use este prompt quando o objetivo principal for:

- descobrir contexto necessário
- planejar antes de executar
- revisar uma solução existente
- validar conformidade de contexto ou saída

Consulte, nesses casos:

- `../discovery/discover-required-context.md`
- `../planning/plan-data-task.md`
- `../review/review-data-solution.md`
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

### Agente
Selecionar um em:
- `../../agents/data-engineering/`
- `../../agents/data-architecture/`

### Regras
Selecionar conforme o objetivo em:
- `../../rules/architecture/`
- `../../rules/coding/`
- `../../rules/modeling/`
- `../../rules/naming/`
- `../../rules/quality/`
- `../../rules/generation/`

### Skills
Selecionar apenas as necessárias em:
- `../../skills/`

---

## Instrução operacional

Ao usar este prompt, o agente SHOULD:

1. identificar o objetivo da geração
2. selecionar o agente adequado
3. carregar `governance/` como base
4. carregar `rules/` relevantes ao tipo de output
5. carregar apenas `skills/` necessárias
6. explicitar lacunas críticas antes de gerar
7. produzir saída clara, rastreável e aderente ao contexto carregado

---

## Saída esperada

A saída SHOULD:

- atender ao objetivo declarado
- respeitar a ordem oficial de composição
- evitar duplicação desnecessária
- respeitar normas carregadas
- não inventar estrutura ausente

---

## Limites

Este prompt inicia geração controlada.

Este prompt não substitui discovery, planejamento, regras, skills ou agentes.
