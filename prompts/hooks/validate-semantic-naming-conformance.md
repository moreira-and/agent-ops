# validate-semantic-naming-conformance

## Tipo do artefato

hook prompt

## Finalidade

Definir checkpoint compacto para validar conformidade de naming semantico antes de merge, deploy ou conclusao de tarefa.

Este hook e um gate. Ele nao e fonte primaria de regra, severidade, unidade ou procedimento tecnico.

---

## Quando usar

Use este hook:

- antes de merge de schema, model, DataFrame ou transformacao
- antes de deploy de mudanca que altera nomes
- antes de concluir revisao de naming
- quando houver risco de quebrar contrato ou linagem por rename

---

## Artefatos minimos

Carregar apenas o necessario:

- `../../rules/naming/README.md`
- `../../rules/naming/_core-pattern.md`
- regras especificas selecionadas pelo roteador
- `../../rules/naming/reference-severity.md`
- `../../rules/naming/reference-units.md` se houver medidas, moeda, quantidade ou unidade
- `../../governance/composition/semantic-naming-governance.md`
- `../../skills/review/semantic-naming-validation.md`

Nao carregar `../../docs/` ou `../../evals/` salvo pedido explicito de exemplo ou validacao.

---

## Entrada obrigatoria

O hook MUST receber:

- artefato ou diff validado
- escopo de nomes avaliados
- contexto semantico disponivel
- restricoes de contrato, se existirem
- relatorio previo de enforcement, se houver

Se a entrada nao permitir decisao segura, retornar `CONDITIONAL`.

---

## Criterio de decisao

### FAIL

Retorne `FAIL` quando:

- existir violacao `CRITICAL`
- houver ambiguidade semantica nao resolvida
- houver rename de contrato externo sem confirmacao humana
- houver violacao `HIGH` sem racional, owner ou acao documentada
- a saida tentar inventar unidade, entidade, tipo ou significado

### CONDITIONAL

Retorne `CONDITIONAL` quando:

- nao ha violacao `CRITICAL`, mas falta contexto para confirmar uma decisao
- violacoes `HIGH` tem racional, mas ainda exigem revisao humana
- o impacto de contrato externo nao foi comprovado

### PASS

Retorne `PASS` quando:

- nenhuma violacao bloqueante permanece
- violacoes nao bloqueantes foram justificadas ou resolvidas
- ambiguidades foram resolvidas explicitamente
- o contexto carregado foi minimo e rastreavel

---

## Saida esperada

```txt
semantic_naming_conformance
status: PASS | FAIL | CONDITIONAL
scope:
artifacts_reviewed:
rules_loaded:
severity_source: ../../rules/naming/reference-severity.md
units_source: ../../rules/naming/reference-units.md | N/A
summary:
  violations_total:
  critical:
  high:
  medium:
  low:
findings:
  - name:
    rule:
    severity:
    evidence:
    decision:
    required_action:
pending_questions:
recommendation: APPROVE | BLOCK | REQUIRES_REVIEW
```

---

## Checkpoints

- [ ] O hook carregou apenas rules e skills necessarias?
- [ ] `reference-severity.md` foi usado como fonte de severidade?
- [ ] `reference-units.md` foi usado quando havia unidade?
- [ ] `CRITICAL` bloqueia?
- [ ] `HIGH` sem racional bloqueia?
- [ ] Ambiguidade nao recebeu auto-fix?
- [ ] O resultado e auditavel por caminho e evidencia?

---

## Exemplos e regressao

Exemplos humanos ficam em:

- `../../docs/examples/semantic-naming-examples.md`

Casos de regressao aplicaveis:

- `../../evals/manual-regression-suite.md` (`EVAL-004`, `EVAL-005`, `EVAL-006`)

---

## Limites

Este hook nao substitui:

- politica de naming
- regras especificas
- procedimento de validacao
- procedimento de deteccao
- procedimento de auto-fix
