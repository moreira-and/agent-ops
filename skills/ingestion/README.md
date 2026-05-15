# ingestion

## Tipo do artefato

discovery

## Finalidade

O diretório `ingestion/` armazena conhecimento operacional reutilizável sobre desenho e estruturação de ingestão de dados.

Este diretório é a fonte primária para capacidades relacionadas a ingestão.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `ingestion/` quando precisar:

- desenhar fluxo de ingestão
- estruturar captura de dados
- orientar ingestão com clareza de etapas
- revisar decisões operacionais de entrada de dados

---

## Quando não usar

Não use `ingestion/` como fonte primária para:

- regras normativas de output
- governança estrutural
- definição de agente
- template de solicitação

Consulte, respectivamente:

- `../../rules/`
- `../../governance/`
- `../../agents/`
- `../../prompts/`

---

## Arquivo primário

- `./ingestion-design.md`

---

## Responsabilidade desta pasta

`ingestion/` MUST conter conhecimento operacional reutilizável sobre ingestão.

`ingestion/` MUST NOT conter regra normativa primária, persona ou governança.

---

## Limites

Este README roteia skills de ingestão.

Este README não substitui `./ingestion-design.md`.
