# quality

## Tipo do artefato

discovery

## Finalidade

O diretório `quality/` define critérios normativos de qualidade para a saída produzida pelos agentes e para entradas humanas que precisam de triagem antes de execução.

Este diretório é a fonte primária para qualidade de output.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`

---

## Quando usar

Consulte `quality/` quando precisar:

- validar se uma saída está aceitável
- avaliar se um pedido humano está claro, seguro e acionável
- reforçar completude e consistência
- revisar risco de ambiguidade
- impor critérios mínimos de qualidade de entrega
- remover bajulacao, concordancia performatica e engajamento artificial

---

## Quando não usar

Não use `quality/` como fonte primária para:

- governança estrutural do repositório
- arquitetura geral
- implementação detalhada
- modelagem específica
- naming

Consulte, respectivamente:

- `../../governance/`
- `../architecture/`
- `../coding/`
- `../modeling/`
- `../naming/`

---

## Arquivos

- `./quality-rules.md`
- `./user-input-quality.md`
- `./neutral-technical-communication.md`

---

## Responsabilidade desta pasta

`quality/` MUST definir critérios normativos de qualidade da saída e da entrada humana quando aplicável.

`quality/` MUST NOT substituir governança estrutural nem padrões especializados de outras áreas.

---

## Limites

Este README roteia critérios de qualidade.

Este README não substitui `./quality-rules.md`, `./user-input-quality.md` nem `./neutral-technical-communication.md`.

## Status v0.1

Este diretorio faz parte da base v0.1 no escopo descrito neste README.

Uso aprovado: piloto profissional controlado. Producao critica exige controles externos de runtime, autorizacao, observabilidade e enforcement fora deste repositorio.
