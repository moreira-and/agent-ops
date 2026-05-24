# architecture

## Tipo do artefato

discovery

## Finalidade

O diretório `architecture/` define as normas arquiteturais que governam a saída produzida pelos agentes.

Este diretório é a fonte primária para restrições de arquitetura no contexto de engenharia de dados.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `architecture/` quando precisar:

- definir ou revisar arquitetura de soluções de dados
- validar separação de responsabilidades
- limitar decomposicao e delegacao de tarefas grandes
- estruturar componentes e interfaces
- orientar decisões arquiteturais de geração

---

## Quando não usar

Não use `architecture/` como fonte primária para:

- governança estrutural do repositório
- convenções de código de baixo nível
- convenções de naming
- critérios gerais de qualidade
- regras de modelagem

Consulte, respectivamente:

- `../../governance/`
- `../coding/`
- `../naming/`
- `../quality/`
- `../modeling/`

---

## Arquivo primário

- `./architecture-rules.md`

## Arquivos

- `./architecture-rules.md`
- `./delegation-boundaries.md`

---

## Responsabilidade desta pasta

`architecture/` MUST definir normas arquiteturais de output.

`architecture/` MUST NOT absorver regras de coding, naming, modeling ou governance.

---

## Limites

Este README roteia normas arquiteturais.

Este README não substitui `./architecture-rules.md` nem `./delegation-boundaries.md`.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
