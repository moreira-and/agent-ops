# generation

## Tipo do artefato

discovery

## Finalidade

O diretório `generation/` define guardrails específicos para geração feita por agentes.

Este diretório é a fonte primária para restrições comportamentais ligadas à geração.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `generation/` quando precisar:

- restringir comportamento de geração
- reduzir alucinação
- reforçar aderência a contexto fornecido
- orientar como o agente deve reagir a lacunas e incertezas

---

## Quando não usar

Não use `generation/` como fonte primária para:

- governança estrutural
- arquitetura da solução
- implementação detalhada
- modelagem
- naming
- qualidade geral

Consulte, respectivamente:

- `../../governance/`
- `../architecture/`
- `../coding/`
- `../modeling/`
- `../naming/`
- `../quality/`

---

## Arquivo primário

- `./generation-guardrails.md`

## Arquivos disponíveis

- `./generation-guardrails.md`
- `./operational-safety-guardrails.md`

---

## Responsabilidade desta pasta

`generation/` MUST definir guardrails comportamentais para geração.

`generation/` MUST NOT substituir regras arquiteturais, de implementação ou de qualidade.

---

## Limites

Este README roteia guardrails de geração.

Este README não substitui guardrails específicos deste diretório.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
