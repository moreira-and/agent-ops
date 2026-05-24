# INDEX feature results

## Tipo do artefato

validation / execution-results

## Finalidade

Registrar a validacao manual da feature `INDEX.md` como roteador barato de discovery inicial por LLM.

Este arquivo valida comportamento. Ele nao define norma primaria.

---

## Escopo

Caso executado:

- `./manual-regression-suite.md` (`EVAL-011`)

Data:

- 2026-05-24

Modo de validacao:

- inspecao documental e simulacao manual do comportamento esperado

Veredito:

```txt
Status: PASS
Feature: INDEX.md como roteador barato de discovery inicial
Restricao: nao normativo, nao enciclopedico e nao carregado por padrao depois da selecao
```

---

## EVAL-011 - INDEX como discovery barato

Entrada:

```txt
Nao sei qual prompt usar para revisar uma solucao de dados. Encontre o ponto de partida sem carregar o repositorio inteiro.
```

Artefatos carregados:

- `../INDEX.md`
- `../governance/composition/context-composition.md`
- `../prompts/README.md`
- `../prompts/review/README.md`

Saida observada:

- `INDEX.md` foi usado somente para escolher o roteador inicial.
- A selecao seguiu para `../prompts/README.md` e `../prompts/review/README.md`.
- `INDEX.md` nao foi tratado como fonte normativa.
- `docs/` e `evals/` nao foram carregados por habito.
- Depois da selecao do roteador especifico, `INDEX.md` deixou de ser necessario no contexto operacional.

Resultado: PASS

Divergencias: nenhuma bloqueante.

Acao tomada: nenhuma.

---

## Limites

Este resultado valida a feature de discovery inicial. Ele nao substitui os resultados de v0.1 em `./v0.1-manual-results.md`.
