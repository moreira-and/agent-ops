# generation

## Tipo do artefato

discovery

## Finalidade

O diretório `generation/` define prompts de entrada para geração de soluções e artefatos no contexto de engenharia de dados.

Este diretório é a fonte primária para prompts de geração.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `generation/` quando precisar:

- iniciar uma geração
- estruturar uma solicitação de construção
- orientar execução com foco em entrega
- acionar composição de contexto para produzir um artefato

---

## Quando não usar

Não use `generation/` como fonte primária para:

- governança estrutural
- regras normativas
- skills operacionais
- definição de agente
- checkpoints de validação

Consulte, respectivamente:

- `../../governance/`
- `../../rules/`
- `../../skills/`
- `../../agents/`
- `../hooks/`

---

## Arquivo primário

- `./generate-data-solution.md`

---

## Responsabilidade desta pasta

`generation/` MUST definir prompts de entrada para geração.

`generation/` MUST NOT substituir regras, skills, governança ou agentes.

---

## Limites

Este README roteia prompts de geração.

Este README não substitui `./generate-data-solution.md`.
