# planning

## Tipo do artefato

discovery

## Finalidade

O diretório `planning/` define prompts de entrada para planejamento antes da execução.

Este diretório é a fonte primária para prompts de planejamento.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `planning/` quando precisar:

- estruturar a abordagem antes de executar
- decompor a tarefa
- validar a composição pretendida
- reduzir improviso na geração ou revisão

---

## Quando não usar

Não use `planning/` como fonte primária para:

- generation final
- review de artefato existente
- discovery inicial de contexto
- checkpoint de validação

Consulte, respectivamente:

- `../generation/`
- `../review/`
- `../discovery/`
- `../hooks/`

---

## Arquivo primário

- `./plan-data-task.md`

---

## Responsabilidade desta pasta

`planning/` MUST definir prompts para planejamento.

`planning/` MUST NOT substituir governança, rules, skills ou agentes.

---

## Limites

Este README roteia prompts de planejamento.

Este README não substitui `./plan-data-task.md`.
