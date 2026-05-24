# semantic-naming-detection

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento operacional para detectar violacoes de naming semantico em codigo, schemas e transformacoes.

Esta skill define tecnica de deteccao. Ela nao define a norma de naming nem a severidade primaria.

---

## Quando usar

Use esta skill quando precisar:

- escanear artefatos em busca de violacoes de naming
- gerar achados com evidencia
- alimentar validacao ou auto-fix
- preparar relatorio de conformidade

---

## Quando nao usar

Nao use esta skill como fonte primaria para:

- politica de naming
- regras especificas
- catalogo de unidades
- matriz de severidade
- decisao de auto-fix

Consulte:

- `../../rules/naming/README.md`
- `../../rules/naming/reference-units.md`
- `../../rules/naming/reference-severity.md`
- `./semantic-naming-validation.md`
- `./semantic-naming-autofix.md`

---

## Pre-condicoes

O agente MUST ter:

- artefato ou lista de nomes a escanear
- escopo de nomes a considerar
- regras selecionadas por `../../rules/naming/README.md`
- contexto semantico quando a deteccao depender de dominio, tipo ou relacionamento

---

## Procedimento

1. Extrair nomes de colunas, variaveis, aliases, tabelas derivadas e campos.
2. Preservar evidencia de origem: arquivo, linha, tabela, coluna ou trecho.
3. Aplicar somente regras selecionadas para o escopo.
4. Detectar violacoes por regra, nao por exemplo decorado.
5. Quando a regra depender de contexto, marcar como `POTENTIAL_VIOLATION` se a evidencia for insuficiente.
6. Classificar severidade por `../../rules/naming/reference-severity.md`.
7. Encaminhar resultado para validacao ou auto-fix.

---

## Sinais de deteccao por regra

| Regra | Sinal de deteccao | Observacao |
|---|---|---|
| `rule-01-format.md` | uppercase, camelCase, caracter invalido, espaco, underscore duplicado | Pode ser detectado por padrao lexical |
| `rule-02-consistency.md` | mesmo conceito com nomes diferentes | Requer comparacao entre artefatos |
| `rule-03-units.md` | valor mensuravel sem unidade explicita | Unidades validas em `reference-units.md` |
| `rule-04-abbreviations.md` | abreviacao proibida ou ambigua | Lista normativa fica na regra especifica |
| `rule-05-no-types.md` | sufixo de tipo tecnico no nome | Exige cuidado com `_date`, que e regra de data |
| `rule-06-booleans.md` | campo booleano sem `is_` ou `has_` | Requer tipo ou evidencia semantica |
| `rule-07-dates.md` | data/timestamp sem sufixo adequado | Requer tipo ou evidencia semantica |
| `rule-08-foreign-keys.md` | `fk_`, `id_<entity>` ou sufixo tecnico de chave | Auto-fix deve ser bloqueado |
| `rule-09-composition-order.md` | ordem diferente de `entity_detail_property_unit` | Requer decomposicao semantica |
| `rule-10-avoid-generic.md` | nome vago ou generico | Requer contexto para sugestao segura |

---

## Sinais lexicais uteis

Use estes sinais como apoio, nao como substituto das regras:

```txt
uppercase_or_invalid: ^[A-Z]|[A-Z]|[^a-z0-9_]|__
technical_fk: ^fk_|^id_[a-z]
generic_exact: ^(data|value|temp|var|result|output|x|y|z|item|thing|stuff|info|obj|attr|prop|field|col)$
type_suffix: _(int|float|string|boolean|timestamp|decimal)$
```

---

## Saida esperada

```txt
semantic_naming_detection
scope:
names_scanned:
rules_applied:
detections:
  - name:
    source:
    rule:
    detection_type: VIOLATION | POTENTIAL_VIOLATION
    evidence:
    required_context:
    severity:
summary:
  total_names:
  detections:
  needs_context:
```

---

## Guardrails

- Nao inventar entidade, unidade, tipo ou relacionamento.
- Nao classificar severidade sem consultar `reference-severity.md`.
- Nao transformar exemplo humano em regra.
- Nao aplicar auto-fix nesta etapa.
- Nao reportar falso positivo critico sem evidencia de contrato, linagem ou consistencia.

---

## Exemplos e regressao

Exemplos completos ficam em:

- `../../docs/examples/semantic-naming-examples.md`

Casos minimos ficam em:

- `../../evals/manual-regression-suite.md`

---

## Limites

Esta skill detecta e estrutura achados. A decisao final de conformidade pertence a `./semantic-naming-validation.md`; auto-fix pertence a `./semantic-naming-autofix.md`.
