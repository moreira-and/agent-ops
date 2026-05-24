# _memory

## Tipo do artefato

discovery / governed memory

## Finalidade

`_memory/` armazena contexto reutilizavel, estavel, pequeno, versionado e auditavel para apoiar continuidade entre execucoes.

Este diretorio e auxiliar. Ele nao faz parte da composicao padrao e nao substitui fontes normativas.

O prefixo `_` indica que esta pasta fica fora das categorias principais do nucleo operacional.

---

## Quando usar

Consulte `_memory/` somente durante `find`, quando:

- houver necessidade recorrente de contexto pequeno e estavel
- uma memory for menor e mais precisa que carregar documentacao maior
- a memory apontar para a fonte primaria correta
- o uso tiver motivo explicito para a tarefa

---

## Quando nao usar

Nao use `_memory/` como:

- fonte normativa primaria
- contexto padrao
- historico bruto de conversa
- substituto de `MANIFEST.md`
- substituto de `governance/`, `rules/`, `skills/`, `prompts/`, `docs/` ou `evals/`

Consulte, respectivamente:

- `../MANIFEST.md`
- `../governance/`
- `../rules/`
- `../skills/`
- `../prompts/`
- `../docs/`
- `../evals/`

---

## Arquivos

- `./project-decisions.md`
- `./stable-preferences.md`
- `./lessons-learned.md`

---

## Status de injecao

condicional

`_memory/` MAY ser descoberta durante `find`.

`_memory/` MUST NOT ser carregada antes de intake.

`_memory/` MUST NOT ser carregada por padrao.

`_memory/` MUST ser descartada quando a fonte primaria especifica for carregada e suficiente.

---

## Precedencia

Em caso de conflito, `_memory/` perde para:

1. `../MANIFEST.md`
2. `../governance/`
3. diretorio especializado aplicavel
4. `../rules/`
5. `../prompts/`
6. `../skills/`
7. `../README.md`
8. `../INDEX.md`

---

## Limites

`_memory/` nao pode conter segredo, credencial, dado pessoal, conversa bruta, log de execucao ou suposicao do agente.

Toda memory deve ter fonte rastreavel, status, escopo, limite e revisao.

## Status v0.1

Este diretorio faz parte da base v0.1 como contexto auxiliar governado e fora da composicao padrao.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
