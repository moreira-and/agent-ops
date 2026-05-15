# composition

## Tipo do artefato

discovery

## Finalidade

O diretório `composition/` define como o contexto do `agent-ops` deve ser descoberto, selecionado, composto e injetado.

Este diretório é a fonte primária para regras de composição contextual.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `composition/` quando precisar:

- entender a ordem oficial de composição
- decidir o que deve ou não ser carregado
- distinguir base padrão de contexto condicional
- reduzir ruído de injeção
- usar checkpoints de validação

---

## Quando não usar

Não use `composition/` como fonte primária para:

- princípios fundacionais gerais
- padrão de escrita dos arquivos
- lifecycle dos artefatos
- critérios de qualidade

Consulte, respectivamente:

- `../principles/core-principles.md`
- `../authoring/markdown-authoring-standard.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../quality/artifact-quality-standard.md`

---

## Arquivo primário

- `./context-composition.md`

---

## Responsabilidade desta pasta

`composition/` MUST definir como o contexto é montado.

`composition/` MUST NOT se tornar fonte primária de princípios genéricos, autoria, lifecycle ou qualidade.

---

## Limites

Este README roteia regras de composição.

Este README não substitui `./context-composition.md`.
