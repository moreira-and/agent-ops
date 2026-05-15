# quality

## Tipo do artefato

discovery

## Finalidade

O diretório `quality/` define critérios normativos de qualidade para a saída produzida pelos agentes.

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
- reforçar completude e consistência
- revisar risco de ambiguidade
- impor critérios mínimos de qualidade de entrega

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

## Arquivo primário

- `./quality-rules.md`

---

## Responsabilidade desta pasta

`quality/` MUST definir critérios normativos de qualidade da saída.

`quality/` MUST NOT substituir governança estrutural nem padrões especializados de outras áreas.

---

## Limites

Este README roteia critérios de qualidade de output.

Este README não substitui `./quality-rules.md`.
