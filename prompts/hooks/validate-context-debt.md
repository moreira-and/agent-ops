# validate-context-debt

## Tipo do artefato

hook prompt

## Status de injecao

condicional

## Finalidade

Validar se um artefato, diretorio ou mudanca aumenta divida de arquitetura informacional.

Este hook implementa o checkpoint operacional de Context Debt Audit.

---

## Quando usar

Use este hook quando:

- o repo parecer redundante, caro ou desorganizado
- uma feature governada gerar varios artefatos novos
- houver duvida se um arquivo agrega valor real
- houver suspeita de responsabilidade misturada
- um artefato parecer no diretorio errado
- uma mudanca tocar roteadores, composition, registry ou evals

---

## Quando nao usar

Nao use este hook quando:

- a mudanca for typo local
- a tarefa for pequena, direta e com criterio local
- a validacao necessaria for apenas qualidade tecnica de output
- o objetivo for executar uma reestruturacao sem auditoria previa

Consulte, respectivamente:

- `../../governance/quality/artifact-quality-standard.md`
- `../../rules/quality/quality-rules.md`
- `../../skills/review/context-architecture-review.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/quality/context-economy-and-responsibility.md`
- `../../governance/composition/context-composition.md`

---

## Artefatos relacionados

- `../../skills/review/context-architecture-review.md`

---

## Instrucao operacional

Ao usar este hook, o agente MUST:

1. identificar o artefato, diretorio ou mudanca avaliada
2. declarar a fonte primaria aplicavel
3. avaliar valor operacional
4. avaliar responsabilidade unica
5. avaliar local correto
6. avaliar redundancia
7. avaliar custo cognitivo e custo de contexto
8. decidir uma saida oficial
9. recomendar ajuste minimo suficiente
10. nao executar remocao, merge, split ou move sem aprovacao ou etapa posterior

---

## Saidas oficiais

Use exatamente uma:

- `KEEP`
- `TRIM`
- `MERGE`
- `MOVE`
- `SPLIT`
- `DEPRECATE`

---

## Saida esperada

```txt
CONTEXT DEBT AUDIT
Status: KEEP | TRIM | MERGE | MOVE | SPLIT | DEPRECATE
Artifact:
Primary source:
Evidence:
Operational value:
Responsibility fit:
Location fit:
Redundancy:
Context cost:
Recommendation:
Required sync targets:
```

---

## Limites

Este hook audita divida de contexto.

Ele nao executa a reestruturacao, nao substitui `../../MANIFEST.md` e nao entra na composicao padrao.
