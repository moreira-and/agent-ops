# Exemplo: composição mínima de contexto

Este exemplo mostra como um humano pode pedir uma execução sem abrir o repositório inteiro.

## Situação

Tarefa: gerar uma solução simples de engenharia de dados.

## Composição

```txt
prompt:
- ./prompts/generation/generate-data-solution.md

governance:
- ./governance/composition/context-composition.md
- ./governance/principles/core-principles.md

agent:
- ./agents/data-engineering/solid-data-engineer.md

rules:
- ./rules/architecture/architecture-rules.md
- ./rules/quality/quality-rules.md
- ./rules/generation/generation-guardrails.md

skills:
- escolher apenas se a tarefa pedir ingestão, transformação, orquestração, modelagem ou revisão
```

## Como pedir ao agente

Peça para ele listar os arquivos carregados, justificar cada escolha e validar no final com:

- `./prompts/hooks/validate-context-and-output.md`

## Erros a evitar

- carregar todos os prompts
- carregar todas as skills
- carregar `./docs/` como contexto padrão
