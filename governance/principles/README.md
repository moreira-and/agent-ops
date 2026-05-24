# principles

## Tipo do artefato

discovery

## Finalidade

O diretório `principles/` define os princípios fundacionais e permanentes do `agent-ops`.

Esses princípios orientam:

- organização do repositório
- decomposição de artefatos
- composição de contexto
- SOLID e injeção de dependências em Markdown
- prevenção de duplicação
- redução de alucinação
- crescimento sustentável

Este diretório é a fonte primária para princípios estruturais.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `principles/` quando precisar:

- entender os princípios permanentes do `agent-ops`
- validar se uma decisão estrutural está correta
- revisar se um artefato respeita a fundação do repositório
- resolver ambiguidades de organização e responsabilidade

---

## Quando não usar

Não use `principles/` como fonte primária para:

- ordem de composição operacional detalhada
- padrão de escrita de arquivos
- política de lifecycle
- critérios de qualidade específicos

Esses conteúdos pertencem, respectivamente, a:

- `../composition/`
- `../authoring/`
- `../lifecycle/`
- `../quality/`

---

## Arquivo primário

- `./core-principles.md`

---

## Responsabilidade desta pasta

`principles/` MUST definir princípios estruturais permanentes.

`principles/` MUST NOT duplicar regras operacionais detalhadas de composição, autoria, lifecycle ou qualidade.

---

## Limites

Este README roteia princípios fundacionais.

Este README não substitui `./core-principles.md`.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
