# Problema: escolher um agente

## Quando isso acontece

Você sabe a tarefa, mas não sabe qual perfil executor deve conduzir a resposta.

## Por que isso importa

O agente define missão, escopo e limites. Usar o perfil errado muda o foco da execução.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: abra o roteador de agentes.
2. Select: escolha o agente pelo tipo de trabalho.
3. Inject: carregue o agente depois de prompt e governance.

## Arquivos que normalmente entram na solução

- `./agents/README.md`
- `./agents/data-engineering/solid-data-engineer.md`
- `./agents/data-architecture/solid-data-architect.md`
- `./agents/data-engineering/semantic-naming-enforcement-agent.md`
- `./agents/agentops-growth-architect.md`

## Erros comuns

- tratar agente como rule
- escolher arquiteto para implementação simples
- escolher engenheiro para decisão arquitetural ampla

## Checklist rápido

- [ ] O agente tem missão compatível com a tarefa.
- [ ] As dependências do agente foram consideradas.
- [ ] Nenhuma skill foi embutida no lugar do agente.
