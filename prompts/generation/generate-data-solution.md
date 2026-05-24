# generate-data-solution

## Tipo do artefato

prompt

## Finalidade

Iniciar a geracao de uma solucao ou artefato de engenharia de dados com composicao contextual controlada.

---

## Quando usar

Use este prompt quando precisar:

- gerar uma solucao nova
- estruturar uma implementacao
- produzir um artefato tecnico com base em contexto selecionado
- conduzir geracao com aderencia ao `agent-ops`

---

## Quando nao usar

Nao use este prompt quando o objetivo principal for:

- descobrir contexto necessario
- planejar antes de executar
- revisar uma solucao existente
- validar conformidade de contexto ou saida

Consulte, nesses casos:

- `../discovery/discover-required-context.md`
- `../planning/plan-data-task.md`
- `../review/review-data-solution.md`
- `../hooks/validate-context-and-output.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../rules/generation/operational-safety-guardrails.md`

---

## Composicao recomendada

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

### Seguranca

Carregar `../../rules/generation/operational-safety-guardrails.md` quando houver execucao, SQL, manipulacao de arquivos, dados sensiveis ou acao destrutiva.

### Skills

Selecionar apenas as necessarias em:

- `../../skills/`

---

## Instrucao operacional

Ao usar este prompt, o agente MUST:

1. identificar o objetivo da geracao
2. validar entradas minimas antes de gerar
3. selecionar o agente adequado
4. carregar `governance/` como base
5. carregar `rules/` relevantes ao tipo de output
6. carregar apenas `skills/` necessarias
7. explicitar lacunas criticas antes de gerar
8. produzir saida clara, rastreavel e aderente ao contexto carregado

---

## Entradas minimas

O agente MUST identificar antes de gerar:

- objetivo
- artefato esperado
- contexto de dominio disponivel
- fonte de dados, sistema ou arquivo de entrada
- destino esperado, consumidor ou sistema de saida
- formato de entrada e saida
- schema, contrato ou campos conhecidos
- volume, latencia ou janela de execucao quando relevante
- restricoes operacionais ou de seguranca
- ferramentas, runtime ou stack permitida quando houver restricao
- criterios minimos de aceite

Se fonte, destino, formato, schema/contrato, qualidade esperada ou restricoes operacionais forem desconhecidos, o agente MUST declarar a lacuna antes de produzir a solucao.

O agente MUST NOT inventar dominio, schema, ferramenta, arquitetura, fonte ou destino para preencher lacuna critica.

---

## Saida esperada

A saida MUST:

- atender ao objetivo declarado
- respeitar a ordem oficial de composicao
- evitar duplicacao desnecessaria
- respeitar normas carregadas
- nao inventar estrutura ausente
- listar lacunas bloqueantes antes de qualquer solucao quando o contexto for insuficiente

Quando houver lacunas bloqueantes, a saida MUST usar:

```txt
generation_readiness
status: CONDITIONAL
blocking_gaps:
  - gap:
    why_it_matters:
    required_input:
safe_next_step:
```

---

## Limites

Este prompt inicia geracao controlada.

Este prompt nao substitui discovery, planejamento, regras, skills ou agentes.
