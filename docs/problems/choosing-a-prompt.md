# Problema: escolher qual prompt usar

## Quando isso acontece

Você tem uma tarefa, mas não sabe se deve gerar, revisar, planejar, descobrir contexto ou executar grow.

## Por que isso importa

Começar pelo prompt errado leva a contexto demais, saída genérica ou execução antes da descoberta.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: leia os roteadores de prompts.
2. Select: escolha um prompt que combine com o tipo de tarefa.
3. Inject: carregue o prompt antes de governance, agent, rules e skills.

## Arquivos que normalmente entram na solução

- `./prompts/README.md`
- `./prompts/discovery/discover-required-context.md`
- `./prompts/generation/generate-data-solution.md`
- `./prompts/review/review-data-solution.md`
- `./prompts/planning/plan-data-task.md`
- `./prompts/grow-from-execution.md`

## Erros comuns

- usar prompt de geração para revisar
- pular discovery quando a tarefa ainda é vaga
- carregar todos os prompts por segurança

## Checklist rápido

- [ ] Sei se a tarefa é discovery, planejamento, geração, revisão ou grow.
- [ ] Escolhi um único prompt principal.
- [ ] O prompt vem primeiro na composição.
