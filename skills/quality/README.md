# quality

## Tipo do artefato

discovery

## Finalidade

O diretório `quality/` armazena conhecimento operacional reutilizável sobre revisão e reforço de qualidade em artefatos de dados.

Este diretório é a fonte primária para capacidades operacionais de qualidade.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `quality/` quando precisar:

- revisar qualidade de uma solução
- estruturar validações relevantes
- orientar verificações de consistência
- reforçar análise crítica de entrega

---

## Quando não usar

Não use `quality/` como fonte primária para:

- regras normativas de qualidade
- governança estrutural
- definição de agente
- prompt de validação

Consulte, respectivamente:

- `../../rules/quality/`
- `../../governance/`
- `../../agents/`
- `../../prompts/hooks/`

---

## Arquivo primário

- `./data-quality-review.md`

---

## Responsabilidade desta pasta

`quality/` MUST conter conhecimento operacional reutilizável sobre revisão de qualidade.

`quality/` MUST NOT substituir regra normativa primária de qualidade.

---

## Limites

Este README roteia skills de qualidade.

Este README não substitui `./data-quality-review.md`.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
