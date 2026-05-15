# Problema: selecionar skills

## Quando isso acontece

Você precisa de técnica operacional, mas não sabe qual skill ajuda.

## Por que isso importa

Skills aumentam capacidade de execução, mas não são normas obrigatórias. Carregar skills erradas aumenta ruído.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: identifique a capacidade operacional necessária.
2. Select: escolha skills úteis para a execução.
3. Inject: carregue skills depois de rules.

## Arquivos que normalmente entram na solução

- `./skills/README.md`
- `./skills/ingestion/ingestion-design.md`
- `./skills/transformation/transformation-design.md`
- `./skills/orchestration/orchestration-design.md`
- `./skills/modeling/data-modeling.md`
- `./skills/quality/data-quality-review.md`
- `./skills/review/technical-review.md`
- `./skills/grow-from-execution.md`

## Erros comuns

- tratar skill como regra
- carregar todas as skills
- usar skill para substituir agente

## Checklist rápido

- [ ] A skill adiciona capacidade útil.
- [ ] A skill não redefine rule.
- [ ] Só carreguei skills necessárias.
