# Problema: selecionar rules

## Quando isso acontece

Você precisa garantir qualidade ou aderência, mas não sabe quais regras aplicar.

## Por que isso importa

Rules são restrições de output. Carregar rules demais aumenta custo; carregar de menos reduz controle.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: identifique o tipo de saída esperada.
2. Select: escolha somente rules ligadas a esse output.
3. Inject: carregue rules depois de prompt, governance e agent.

## Arquivos que normalmente entram na solução

- `./rules/README.md`
- `./rules/architecture/architecture-rules.md`
- `./rules/coding/coding-rules.md`
- `./rules/modeling/modeling-rules.md`
- `./rules/naming/README.md`
- `./rules/quality/quality-rules.md`
- `./rules/generation/generation-guardrails.md`
- `./rules/growth-artifact-quality.md`

## Erros comuns

- usar skill como regra obrigatória
- carregar todo `./rules/`
- ignorar o roteador de naming antes de escolher regras específicas

## Checklist rápido

- [ ] A rule restringe output.
- [ ] A rule é relevante para a saída.
- [ ] Não carreguei rules por hábito.
