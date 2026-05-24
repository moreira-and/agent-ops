# semantic-naming-validation

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento reutilizavel para validar conformidade de nomes contra `rules/naming/`.

Esta skill define tecnica de validacao. Ela nao define politica, regra primaria, severidade primaria ou catalogo de unidades.

---

## Quando usar

Use esta skill quando precisar:

- validar um conjunto de nomes
- revisar conformidade antes de merge
- estruturar uma validacao manual ou assistida
- produzir relatorio de naming com evidencia

---

## Quando nao usar

Nao use esta skill como fonte primaria para:

- politica de naming
- regra especifica
- severidade
- unidades validas
- deteccao automatica
- auto-fix

Consulte:

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `../../rules/naming/reference-severity.md`
- `../../rules/naming/reference-units.md`
- `./semantic-naming-detection.md`
- `./semantic-naming-autofix.md`

---

## Pre-condicoes

Antes de validar, o agente MUST ter:

- lista de nomes ou artefato de origem
- escopo da validacao
- contexto semantico disponivel
- rules selecionadas por `../../rules/naming/README.md`
- criterio de severidade em `../../rules/naming/reference-severity.md`

---

## Procedimento

1. Extrair nomes do artefato: colunas, variaveis, aliases, tabelas derivadas ou campos.
2. Normalizar a lista de nomes sem alterar o artefato original.
3. Identificar quais regras de `../../rules/naming/` se aplicam ao escopo.
4. Validar formato contra `../../rules/naming/_core-pattern.md` e regras selecionadas.
5. Validar consistencia semantica usando o contexto fornecido.
6. Validar unidades contra `../../rules/naming/reference-units.md` quando houver valor mensuravel.
7. Classificar severidade usando apenas `../../rules/naming/reference-severity.md`.
8. Marcar casos sem contexto suficiente como `CONDITIONAL`, nao como conformes.
9. Produzir relatorio estruturado.

---

## Checklist compacto

- [ ] O nome segue o padrao core aplicavel?
- [ ] O nome e lowercase e snake_case?
- [ ] O mesmo conceito usa o mesmo nome?
- [ ] Valores mensuraveis declaram unidade valida?
- [ ] Abreviacoes proibidas foram detectadas?
- [ ] Tipos de dados nao estao codificados no nome?
- [ ] Booleanos usam `is_` ou `has_` quando aplicavel?
- [ ] Datas usam `_date` ou `_at` quando aplicavel?
- [ ] Chaves estrangeiras usam `<referenced_entity>_id`?
- [ ] Nomes compostos respeitam hierarquia semantica?
- [ ] Nomes genericos foram sinalizados?

---

## Saida esperada

```txt
semantic_naming_validation
status: PASS | FAIL | CONDITIONAL
scope:
names_reviewed:
rules_applied:
findings:
  - name:
    rule:
    severity:
    evidence:
    rationale:
    suggested_action:
pending_context:
recommendation:
```

---

## Guardrails

- Nao inferir significado de negocio ausente.
- Nao aceitar unidade implicita.
- Nao reduzir severidade localmente.
- Nao usar exemplos de `docs/` como regra primaria.
- Nao concluir `PASS` se houver ambiguidade relevante sem decisao documentada.

---

## Exemplos e regressao

Exemplos completos ficam em:

- `../../docs/examples/semantic-naming-examples.md`

Casos minimos ficam em:

- `../../evals/manual-regression-suite.md`

---

## Limites

Esta skill fornece procedimento de validacao. Ela nao substitui deteccao, auto-fix, regras especificas ou governanca.
