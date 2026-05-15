# Problema: reduzir uso de tokens

## Quando isso acontece

O agente está carregando arquivos demais ou repetindo contexto que não ajuda a tarefa.

## Por que isso importa

Contexto excessivo aumenta custo, reduz foco e pode confundir modelos menores.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: descubra candidatos sem abrir tudo.
2. Select: escolha o menor conjunto suficiente.
3. Inject: carregue apenas o que tem função clara.

## Arquivos que normalmente entram na solução

- `./prompts/discovery/discover-required-context.md`
- `./governance/composition/context-composition.md`
- `./prompts/hooks/validate-context-and-output.md`
- `./rules/generation/generation-guardrails.md`

## Erros comuns

- carregar todos os diretórios
- carregar todas as rules de naming sem necessidade
- carregar skills por hábito

## Checklist rápido

- [ ] Cada arquivo carregado tem motivo.
- [ ] Removi contexto opcional irrelevante.
- [ ] O hook apontou excesso ou lacuna.
