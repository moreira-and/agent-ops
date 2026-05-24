# rule-08-foreign-keys

## Tipo do artefato

rule

## Finalidade

Definir o padrao obrigatorio para nomes de chaves estrangeiras.

Esta regra define a obrigacao. A severidade e a acao bloqueante sao consultadas em `./reference-severity.md`.

---

## Quando usar

Use esta regra quando precisar:

- nomear colunas de chave estrangeira
- validar referencias entre entidades
- revisar risco de join, linhagem ou contrato externo
- implementar linter de chaves

---

## Quando nao usar

Nao use esta regra como fonte primaria para:

- padrao fundamental de todos os nomes
- consistencia semantica geral
- severidade
- procedimento de auto-fix

Consulte:

- `./_core-pattern.md`
- `./rule-02-consistency.md`
- `./reference-severity.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Regra

Chaves estrangeiras MUST usar o padrao:

```txt
<referenced_entity>_id
```

O nome deve representar a entidade referenciada, nao o mecanismo tecnico da chave.

---

## Padroes proibidos

| Padrao proibido | Motivo |
|---|---|
| `fk_<entity>` | prefixo tecnico |
| `id_<entity>` | ordem invertida |
| `<entity>_fk` | sufixo tecnico |
| `<entity>_key` | sufixo tecnico |
| `<abbreviation>_id` | abreviacao ambigua |

---

## Criterio de conformidade

Um nome esta conforme quando:

- identifica a entidade referenciada
- usa `<referenced_entity>_id`
- e consistente com a tabela ou entidade de referencia
- nao codifica mecanismo tecnico (`fk`, `key`, `ref`)

Um nome nao esta conforme quando:

- usa prefixo ou sufixo tecnico
- inverte a ordem da entidade e do identificador
- usa abreviacao para a entidade referenciada
- cria inconsistencia entre tabelas ou contratos

---

## Severidade

A severidade desta regra MUST ser consultada em `./reference-severity.md`.

`./reference-severity.md` mapeia violacao desta regra como `CRITICAL`.

---

## Auto-fix

Renomear chave estrangeira MUST ser bloqueado por padrao.

Motivo: pode quebrar queries em producao, APIs, linagem, documentacao, migracoes ou contratos externos.

Procedimento de decisao: `../../skills/review/semantic-naming-autofix.md`.

---

## Saida minima esperada em validacao

```txt
name:
rule: rule-08-foreign-keys.md
expected_pattern: <referenced_entity>_id
severity_source: ./reference-severity.md
decision: BLOCKED | REQUIRES_REVIEW | PASS
evidence:
rationale:
```

---

## Limites

Esta regra governa chaves estrangeiras. Ela nao governa formato geral, unidades, abreviacoes gerais, tipos, booleanos ou nomes genericos.
