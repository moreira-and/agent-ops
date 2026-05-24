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
- classificar impacto de mudança e revisar sync targets
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

## Arquivos

- `./artifact-lifecycle-policy.md`
- `./artifact-synchronization-policy.md`

---

## Responsabilidade desta pasta

`lifecycle/` MUST governar a evolução dos artefatos.

`lifecycle/` MUST definir como sincronizar artefatos impactados por mudanças relevantes.

`lifecycle/` MUST NOT duplicar padrão de autoria, composição ou qualidade.

---

## Limites

Este README roteia política de lifecycle.

Este README não substitui `./artifact-lifecycle-policy.md` nem `./artifact-synchronization-policy.md`.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
