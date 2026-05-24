# semantic-naming-autofix

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento operacional para decidir e aplicar auto-fix de naming semantico somente quando a transformacao for deterministica, local e de baixo risco.

Esta skill define a tecnica de auto-fix. Ela nao define politica, regra primaria, severidade primaria ou catalogo de unidades.

---

## Quando usar

Use esta skill quando precisar:

- separar correcao automatica de revisao humana
- aplicar transformacoes lexicais seguras
- bloquear renames com risco semantico ou contratual
- documentar racional de correcao

---

## Quando nao usar

Nao use esta skill para:

- inferir significado de negocio
- escolher unidade sem evidencia
- renomear contrato externo sem aprovacao
- substituir regras em `../../rules/naming/`

Consulte:

- `../../rules/naming/README.md`
- `../../rules/naming/reference-severity.md`
- `../../rules/naming/reference-units.md`
- `./semantic-naming-detection.md`
- `./semantic-naming-validation.md`

---

## Principio de auto-fix

Auto-fix e permitido apenas quando todas as condicoes forem verdadeiras:

- transformacao e deterministica
- significado semantico nao muda
- impacto e local e de baixo risco
- nao ha contrato externo conhecido
- evidencia de tipo, unidade ou entidade e suficiente quando necessaria

Caso contrario, o resultado MUST ser `REQUIRES_REVIEW` ou `BLOCKED`.

---

## Matriz operacional

| Transformacao | Condicao minima | Decisao padrao |
|---|---|---|
| `camel_case_to_snake_case` | apenas formato lexical | AUTO_FIXABLE |
| `normalize_case` | apenas casing | AUTO_FIXABLE |
| `remove_accents` | transliteracao direta | AUTO_FIXABLE |
| `collapse_double_underscore` | separador duplicado | AUTO_FIXABLE |
| `remove_type_suffix` | tipo tecnico redundante e sem conflito com regra de data | AUTO_FIXABLE |
| `expand_abbreviation` | abreviacao com significado unico no contexto | CONDITIONAL |
| `add_boolean_prefix` | tipo BOOLEAN confirmado e sem ambiguidade | CONDITIONAL |
| `add_date_suffix` | tipo DATE/TIMESTAMP confirmado e sem ambiguidade | CONDITIONAL |
| `add_unit` | unidade explicitamente informada por contrato ou contexto confiavel | BLOCKED_BY_DEFAULT |
| `standardize_foreign_key` | chave ou contrato externo envolvido | BLOCKED |
| `rename_generic` | requer significado de negocio | BLOCKED_BY_DEFAULT |
| `reorder_components` | decomposicao semantica inequivoca | CONDITIONAL |

---

## Procedimento

Para cada deteccao:

1. Identificar a regra violada e a severidade em `../../rules/naming/reference-severity.md`.
2. Identificar se ha contrato externo, linagem, query publica, API ou migracao envolvida.
3. Escolher a transformacao aplicavel na matriz operacional.
4. Se `AUTO_FIXABLE`, aplicar apenas a mudanca local e documentar racional.
5. Se `CONDITIONAL`, aplicar somente com evidencia explicita no input.
6. Se `BLOCKED` ou `BLOCKED_BY_DEFAULT`, nao alterar o artefato; sugerir alternativas e pedir decisao humana.
7. Produzir relatorio auditavel.

---

## Guardrails

- Nao adicionar unidade por suposicao.
- Nao padronizar chave estrangeira automaticamente.
- Nao renomear nome generico sem contexto de negocio.
- Nao aplicar auto-fix que altere contrato publico.
- Nao aplicar auto-fix em lote sem diff rastreavel.
- Nao usar exemplos de `docs/` como autorizacao para uma decisao.

---

## Saida esperada

```txt
semantic_naming_autofix
status: PASS | CONDITIONAL | BLOCKED
changes:
  - original_name:
    new_name:
    transformation:
    decision: AUTO_FIXABLE | REQUIRES_REVIEW | BLOCKED
    evidence:
    risk:
    rationale:
blocked:
  - original_name:
    suggested_options:
    reason:
pending_questions:
summary:
```

---

## Validacao antes de aplicar

Antes de alterar qualquer nome, validar:

- [ ] O novo nome segue `../../rules/naming/_core-pattern.md`?
- [ ] A severidade foi consultada em `reference-severity.md`?
- [ ] Unidade, tipo e entidade estao evidentes?
- [ ] Nao ha contrato externo ou impacto de linagem?
- [ ] O diff pode ser auditado por humano?

---

## Exemplos e regressao

Exemplos completos ficam em:

- `../../docs/examples/semantic-naming-examples.md`

Casos minimos ficam em:

- `../../evals/manual-regression-suite.md` (`EVAL-005`, `EVAL-006`)

---

## Limites

Esta skill decide auto-fix. Ela nao detecta violacoes sozinha e nao declara conformidade final.
