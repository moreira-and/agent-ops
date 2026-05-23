# review-data-solution

## Tipo do artefato

prompt

## Finalidade

Iniciar a revisão de uma solução ou artefato existente com composição contextual controlada.

---

## Quando usar

Use este prompt quando precisar:

- revisar implementação existente
- revisar desenho de solução
- validar coerência, clareza e aderência normativa
- estruturar análise crítica antes de concluir

---

## Quando não usar

Não use este prompt quando o objetivo principal for:

- gerar do zero
- descobrir contexto necessário
- planejar uma nova execução
- validar checkpoint de conformidade final

Consulte, nesses casos:

- `../generation/generate-data-solution.md`
- `../discovery/discover-required-context.md`
- `../planning/plan-data-task.md`
- `../hooks/validate-context-and-output.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../rules/quality/quality-rules.md`

---

## Composição recomendada

### Base
- `../../governance/principles/core-principles.md`
- `../../governance/composition/context-composition.md`

### Agente
Selecionar conforme o foco da revisão em:
- `../../agents/data-engineering/`
- `../../agents/data-architecture/`

### Regras
Selecionar conforme o artefato revisado em:
- `../../rules/`

### Skills
Selecionar quando necessário em:
- `../../skills/review/`
- `../../skills/quality/`
- outras áreas relevantes de `../../skills/`

---

## Instrução operacional

Ao usar este prompt, o agente MUST:

1. identificar o tipo de artefato revisado
2. selecionar o agente mais adequado para a revisão
3. carregar regras pertinentes ao tipo de saída
4. usar skills de revisão apenas quando agregarem precisão
5. explicitar problemas, riscos, lacunas e conflitos de forma objetiva
6. evitar reescrever normas já definidas em suas fontes primárias

---

## Entradas mínimas

O agente MUST identificar antes de revisar:

- artefato revisado
- objetivo da revisão
- regras aplicáveis
- critérios mínimos de aceite
- riscos operacionais, quando houver

Se o artefato ou objetivo não estiver claro, o agente MUST declarar a lacuna antes de emitir veredito.

---

## Saída esperada

A saída MUST:

- apontar achados relevantes
- distinguir problema de sugestão
- citar evidência concreta para achados
- declarar impacto técnico
- recomendar ação objetiva
- referenciar regras e limites aplicáveis quando necessário
- reduzir ambiguidade
- apoiar decisão ou correção posterior

---

## Limites

Este prompt inicia revisão de solução existente.

Este prompt não substitui hooks de conformidade nem skills especializadas de revisão.
