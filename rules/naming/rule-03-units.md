# rule-03-units

## Tipo do artefato

rule

## Finalidade

Definir a obrigacao de declarar unidade explicita em nomes de valores mensuraveis.

Esta regra define a obrigacao. O catalogo de unidades validas fica em `./reference-units.md`.

---

## Quando usar

Use esta regra quando precisar:

- validar nomes de medidas, moedas, quantidades, duracoes ou grandezas fisicas
- identificar ambiguidade causada por unidade ausente
- revisar conformidade de campos mensuraveis

---

## Quando nao usar

Nao use esta regra como fonte primaria para:

- catalogo de unidades validas
- severidade
- procedimento de deteccao
- procedimento de auto-fix

Consulte:

- `./reference-units.md`
- `./reference-severity.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Regra

Valores mensuraveis MUST incluir unidade explicita no nome.

Exemplos de conceitos que exigem unidade:

- peso ou massa
- volume
- temperatura
- distancia
- moeda ou valor monetario
- duracao
- percentual
- velocidade
- pressao
- densidade
- concentracao

Unidades validas MUST ser consultadas em `./reference-units.md`.

---

## Criterio de conformidade

Um nome esta conforme quando:

- representa valor mensuravel
- declara unidade ou moeda explicitamente
- a unidade existe em `./reference-units.md` ou foi documentada como extensao de dominio
- a unidade nao contradiz o contexto semantico

Um nome nao esta conforme quando:

- representa valor mensuravel sem unidade
- usa unidade ambigua ou nao documentada
- usa sufixo generico como `value`, `amount` ou `total` sem unidade/moeda quando o dominio exige precisao

---

## Severidade

A severidade desta regra MUST ser consultada em `./reference-severity.md`.

---

## Auto-fix

Unidade ausente MUST NOT receber auto-fix por suposicao.

Auto-fix so pode ser considerado quando a unidade estiver explicitamente presente no input, contrato, schema, metadado confiavel ou decisao humana registrada.

Procedimento de decisao: `../../skills/review/semantic-naming-autofix.md`.

---

## Saida minima esperada em validacao

```txt
name:
rule: rule-03-units.md
evidence:
severity_source: ./reference-severity.md
unit_source: ./reference-units.md
decision: PASS | REQUIRES_REVIEW | BLOCKED
rationale:
```

---

## Limites

Esta regra governa a obrigacao de unidade. Ela nao governa formato geral, consistencia, abreviacoes, tipos, booleanos ou chaves estrangeiras.
