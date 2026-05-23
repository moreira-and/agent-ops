# Template: novo artefato

Use este template antes de criar qualquer novo `.md`.

O objetivo e reduzir improviso. Nao copie secoes que nao agregam clareza ao caso.

```md
# <nome-do-artefato>

## Tipo do artefato

<discovery | governance | agent | rule | skill | prompt | hook prompt | validation | human documentation>

## Status de injecao

<padrao | condicional | nao injetavel>

## Finalidade

<por que este arquivo existe>

---

## Quando usar

- <situacao objetiva>

---

## Quando nao usar

- <limite objetivo>

Consulte:

- `<caminho-da-fonte-correta>`

---

## Dependencias relacionadas

- `<caminho>`

---

## Instrucao ou contrato

<conteudo principal>

---

## Saida esperada

<quando aplicavel>

---

## Limites

<o que este arquivo nao substitui>
```

## Checklist

- [ ] Ha responsabilidade principal clara.
- [ ] O diretorio escolhido e correto.
- [ ] Nao existe fonte primaria equivalente.
- [ ] Dependencias estao por caminho.
- [ ] O arquivo pode ser selecionado sem leitura global.
- [ ] `docs/` e `evals/` nao viraram contexto padrao.
