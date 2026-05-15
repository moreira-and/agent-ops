# lifecycle

## Tipo do artefato

discovery

## Finalidade

O diretório `lifecycle/` define como artefatos do `agent-ops` devem ser criados, alterados, divididos, consolidados, movidos e removidos.

Este diretório é a fonte primária para lifecycle dos artefatos.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `lifecycle/` quando precisar:

- decidir se um novo arquivo deve existir
- dividir um artefato
- consolidar conteúdo
- mover ou remover arquivos
- controlar crescimento do repositório

---

## Quando não usar

Não use `lifecycle/` como fonte primária para:

- princípios fundacionais
- composição de contexto
- padrão de autoria
- critérios de qualidade

Consulte, respectivamente:

- `../principles/core-principles.md`
- `../composition/context-composition.md`
- `../authoring/markdown-authoring-standard.md`
- `../quality/artifact-quality-standard.md`

---

## Arquivo primário

- `./artifact-lifecycle-policy.md`

---

## Responsabilidade desta pasta

`lifecycle/` MUST governar a evolução dos artefatos.

`lifecycle/` MUST NOT duplicar padrão de autoria, composição ou qualidade.

---

## Limites

Este README roteia política de lifecycle.

Este README não substitui `./artifact-lifecycle-policy.md`.
