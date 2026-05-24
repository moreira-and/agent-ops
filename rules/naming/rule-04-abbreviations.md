# rule-04-abbreviations

## Tipo do artefato

rule

## Finalidade

Definir quando abreviacoes sao proibidas ou permitidas em nomes semanticos.

Esta regra define a obrigacao. Decisao de auto-fix pertence a `../../skills/review/semantic-naming-autofix.md`.

---

## Quando usar

Use esta regra quando precisar:

- validar se um nome usa abreviacao ambigua
- revisar legibilidade de identificadores
- diferenciar abreviacao tecnica aceitavel de nome semantico ruim
- implementar linter de abreviacoes

---

## Quando nao usar

Nao use esta regra como fonte primaria para:

- padrao fundamental
- formato lexical
- consistencia semantica
- unidades validas
- decisao de auto-fix

Consulte:

- `./_core-pattern.md`
- `./rule-01-format.md`
- `./rule-02-consistency.md`
- `./reference-units.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Regra

Nomes semanticos MUST NOT usar abreviacoes ambiguas.

Apenas abreviacoes universalmente reconhecidas ou codigos padronizados de dominio podem ser usados, desde que nao escondam significado de negocio.

---

## Abreviacoes proibidas em nomes semanticos

| Proibido | Motivo |
|---|---|
| `dt` | ambiguo entre data, datetime ou detalhe |
| `vlr` | ambiguo entre valor, volume ou outro conceito local |
| `cod` | ambiguo entre codigo, codificacao ou convencao legada |
| `qtd` | ambiguo e dependente de idioma |
| `desc` | ambiguo entre descricao e desconto |
| `cust` | ambiguo entre customer e custom |
| `prod` | ambiguo entre product e production |
| `inv` | ambiguo entre invoice e inventory |
| `addr` | abreviacao desnecessaria de address |
| `tel` | ambiguo entre telefone e telemetria |
| `doc` | ambiguo entre document e outros dominios |
| `ref` | ambiguo entre reference, refund ou referral |
| `val` | ambiguo entre value e validation |
| `num` | ambiguo e geralmente redundante |
| `seq` | ambiguo e dependente de convencao local |
| `avg`, `cnt`, `amt` | abreviacoes tecnicas; prefira nome completo salvo contrato explicito |

---

## Abreviacoes permitidas

Permitidas quando fazem parte de padrao amplamente reconhecido:

- `id` em identificadores semanticos, como `customer_id`
- moedas ISO 4217, como `brl`, `usd`, `eur`
- unidades reconhecidas em `./reference-units.md`, como `kg`, `km`, `ml`
- `fk` e `pk` apenas em nomes de constraints tecnicas, nao em nomes semanticos de colunas

---

## Criterio de conformidade

Um nome esta conforme quando:

- nao usa abreviacao ambigua;
- usa abreviacao permitida apenas no contexto autorizado;
- preserva significado semantico legivel;
- nao mistura idioma ou convencao local sem contrato explicito.

Um nome nao esta conforme quando:

- depende de conhecimento tribal para ser entendido;
- usa abreviacao proibida;
- usa `fk`/`pk` como nome semantico de coluna;
- tenta corrigir abreviacao sem resolver unidade, moeda, entidade ou significado.

---

## Severidade

A severidade desta regra MUST ser consultada em `./reference-severity.md`.

---

## Auto-fix

Abreviacao proibida MUST NOT autorizar auto-fix isolado quando houver ambiguidade de unidade, moeda, entidade, idioma ou contrato.

Auto-fix so pode ser considerado quando:

- a expansao e inequivoca no contexto fornecido;
- nenhuma regra de unidade, chave, consistencia ou contrato fica pendente;
- o procedimento em `../../skills/review/semantic-naming-autofix.md` classifica a mudanca como segura ou condicional atendida.

Caso contrario, a decisao MUST ser `REQUIRES_REVIEW` ou `BLOCKED`.

---

## Saida minima esperada em validacao

```txt
name:
rule: rule-04-abbreviations.md
abbreviation:
severity_source: ./reference-severity.md
decision: PASS | REQUIRES_REVIEW | BLOCKED
evidence:
rationale:
```

---

## Limites

Esta regra governa abreviacoes. Ela nao governa formato geral, unidades, tipos, booleanos, datas, chaves estrangeiras ou nomes genericos.
