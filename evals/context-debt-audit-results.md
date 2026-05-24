# Context Debt Audit results

## Tipo do artefato

validation / human-review

## Finalidade

Registrar validacao manual de Context Debt Audit.

Este arquivo e evidencia de validacao. Ele nao e fonte normativa primaria e nao deve ser carregado por padrao em execucoes agenticas.

---

## Fonte da suite

- `./manual-regression-suite.md` (`EVAL-017`)

---

## Escopo

- `../prompts/hooks/validate-context-debt.md`
- `../governance/quality/context-economy-and-responsibility.md`
- `../skills/review/context-architecture-review.md`
- `../governance/composition/context-composition.md`
- `../README.md`
- `../INDEX.md`

---

## Resultado

```txt
Eval ID: EVAL-017
Data: 2026-05-24
Executor: Codex
Modo de validacao: inspecao manual de contrato
Artefatos carregados: prompts/hooks/validate-context-debt.md; governance/quality/context-economy-and-responsibility.md; skills/review/context-architecture-review.md; governance/composition/context-composition.md; evals/manual-regression-suite.md
Entrada usada: EVAL-017 casos 1-5
Saida observada: casos 1-5 PASS conforme tabela de casos avaliados
Resultado: PASS
Divergencias: nenhuma bloqueante
Acao recomendada: manter Context Debt Audit sob demanda e fora da composicao padrao
```

---

## Casos avaliados

| Caso | Entrada | Resultado esperado | Resultado observado |
|---|---|---|---|
| 1 | Hook curto e bem localizado | `KEEP` | PASS |
| 2 | README copia spec inteira | `TRIM` ou `MERGE` | PASS |
| 3 | Skill contem regra normativa | `MOVE`, `TRIM` ou `SPLIT` | PASS |
| 4 | Eval explica policy | `TRIM` ou `MOVE` | PASS |
| 5 | Novo diretorio raiz sem justificativa | Bloquear crescimento estrutural | PASS |

---

## Veredito

Status: PASS.

Context Debt Audit esta governado como auditoria sob demanda para conter crescimento, redundancia, local incorreto e custo cognitivo. A feature recomenda ajustes, mas nao executa reestruturacao automaticamente.
