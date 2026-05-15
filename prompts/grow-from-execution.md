# grow-from-execution

## Tipo do artefato

prompt

## Status de injeção

condicional

## Finalidade

Conduzir o fluxo `grow` a partir de um arquivo `.md` que registre uma execução anterior.

Este prompt transforma execução passada em proposta controlada de evolução do `agent-ops`.

---

## Quando usar

Use este prompt quando precisar:

- analisar relatório, auditoria, retrospectiva ou plano executado
- extrair conhecimento reutilizável de uma execução anterior
- propor novos prompts, agents, rules, skills, hooks ou governance
- atualizar artefatos existentes com baixo risco
- rejeitar conhecimento que não deve virar contexto injetável

---

## Quando não usar

Não use este prompt para:

- copiar conteúdo bruto de execução para o repositório
- registrar histórico humano em `../docs/`
- criar regra global sem recorrência ou evidência
- executar tarefa técnica que não envolva evolução do `agent-ops`

Consulte, nesses casos:

- `./review/review-data-solution.md`
- `./planning/plan-data-task.md`
- `./hooks/validate-context-and-output.md`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/principles/core-principles.md`
- `../governance/composition/context-composition.md`
- `../governance/lifecycle/artifact-lifecycle-policy.md`
- `../governance/authoring/markdown-authoring-standard.md`
- `../governance/quality/artifact-quality-standard.md`
- `../agents/agentops-growth-architect.md`
- `../rules/growth-artifact-quality.md`
- `../skills/grow-from-execution.md`
- `./hooks/validate-growth-proposal.md`

---

## Precedência

Este prompt inicia o fluxo.

Ele deve respeitar a ordem:

```txt
prompt -> governance -> agent -> rules -> skills
```

---

## Entrada esperada

O agente MUST receber:

- caminho do arquivo `.md` de execução
- objetivo do grow, se houver
- autorização explícita para criar ou alterar artefatos, quando a execução sair da fase de proposta

O arquivo de execução MAY conter:

- relatório de execução
- plano executado
- auditoria realizada
- correção aplicada
- retrospectiva técnica
- decisão arquitetural
- análise de lacunas
- revisão de repositório

---

## Composição recomendada

### Prompt
- `./grow-from-execution.md`

### Governance
- `../MANIFEST.md`
- `../governance/principles/core-principles.md`
- `../governance/composition/context-composition.md`
- `../governance/lifecycle/artifact-lifecycle-policy.md`
- `../governance/authoring/markdown-authoring-standard.md`
- `../governance/quality/artifact-quality-standard.md`

### Agent
- `../agents/agentops-growth-architect.md`

### Rules
- `../rules/growth-artifact-quality.md`
- rules específicas conforme o tipo de artefato a criar ou atualizar

### Skills
- `../skills/grow-from-execution.md`

### Hook
- `./hooks/validate-growth-proposal.md`

---

## Instrução operacional

Ao usar este prompt, o agente SHOULD:

1. ler o arquivo `.md` de execução
2. separar conhecimento reutilizável de histórico bruto
3. classificar cada candidato pela matriz de decisão
4. verificar se já existe artefato equivalente
5. decidir entre criar, atualizar, mover, consolidar ou rejeitar
6. produzir plano antes de alterar arquivos
7. implementar apenas mudanças justificadas e de baixo risco
8. validar a proposta com `./hooks/validate-growth-proposal.md`
9. reportar artefatos criados, alterados e rejeitados

---

## Matriz de classificação

| Conhecimento identificado | Destino |
|---------------------------|---------|
| tarefa ou fluxo de entrada | prompt |
| perfil executor, missão, escopo ou limites | agent |
| obrigação de saída, restrição ou guardrail | rule |
| técnica, heurística ou procedimento reutilizável | skill |
| validação de checkpoint | hook |
| estrutura, autoria, composição ou evolução do `agent-ops` | governance |
| explicação histórica ou referência humana | docs ou rejeição |
| caso pontual sem recorrência | rejeição |

---

## Critérios de rejeição

Rejeite conhecimento quando ele for:

- contexto bruto de execução
- pontual demais
- sem evidência no `.md` de origem
- duplicado em artefato existente
- opinião não generalizável
- específico de vendor, modelo ou framework
- exemplo que não melhora execução
- regra já existente com outra redação

---

## Saída esperada

A saída SHOULD conter:

- resumo do arquivo de execução analisado
- candidatos reutilizáveis encontrados
- candidatos rejeitados e motivo
- matriz de classificação aplicada
- artefatos existentes relacionados
- plano antes da alteração
- alterações realizadas, se autorizadas
- validação final

---

## Limites

Este prompt conduz o fluxo `grow`.

Este prompt não substitui:

- governança de lifecycle
- regra de qualidade para grow
- skill operacional de destilação
- agente executor especializado
- documentação humana em `../docs/`
