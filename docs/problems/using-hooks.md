# Problema: saber quando usar um hook

## Quando isso acontece

Você quer validar contexto, saída ou uma proposta antes de concluir.

## Por que isso importa

Hooks são checkpoints. Usar hook como prompt principal confunde o fluxo.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: identifique o risco a validar.
2. Select: escolha o hook específico.
3. Inject: acione o hook como checkpoint, não como base obrigatória.

## Arquivos que normalmente entram na solução

- `./prompts/hooks/README.md`
- `./prompts/hooks/validate-context-and-output.md`
- `./prompts/hooks/validate-semantic-naming-conformance.md`
- `./prompts/hooks/validate-growth-proposal.md`

## Erros comuns

- iniciar uma tarefa pelo hook
- validar sem carregar as rules aplicáveis
- pular hook quando há risco de conformidade

## Checklist rápido

- [ ] O hook valida um checkpoint claro.
- [ ] O prompt principal já foi escolhido.
- [ ] A validação aponta para rules ou governance reais.
