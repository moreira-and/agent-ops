# Problema: corrigir seleção de contexto

## Quando isso acontece

O agente escolheu arquivos demais, arquivos errados ou deixou faltar contexto importante.

## Por que isso importa

Seleção ruim causa resposta genérica, conflito normativo ou violação de regra.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: liste a tarefa e os artefatos candidatos.
2. Select: remova arquivos sem função clara.
3. Inject: valide suficiência e excesso antes de concluir.

## Arquivos que normalmente entram na solução

- `./prompts/discovery/discover-required-context.md`
- `./governance/composition/context-composition.md`
- `./prompts/hooks/validate-context-and-output.md`
- `./rules/generation/generation-guardrails.md`

## Erros comuns

- não diferenciar base padrão e contexto condicional
- carregar `./docs/` como contexto padrão
- usar hook no lugar do prompt principal

## Checklist rápido

- [ ] Cada arquivo tem motivo explícito.
- [ ] O contexto segue a ordem oficial.
- [ ] `./docs/` ficou fora da composição padrão.
