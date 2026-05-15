# Problema: usar o grow

## Quando isso acontece

Você tem um `.md` de execução anterior e quer transformar aprendizados recorrentes em artefatos reutilizáveis.

## Por que isso importa

Grow sem controle vira memória bruta, duplica normas e aumenta contexto obrigatório.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: localize o arquivo de execução e os artefatos de grow.
2. Select: carregue prompt, governance, agent, rule e skill de grow.
3. Inject: valide a proposta antes de alterar.

## Arquivos que normalmente entram na solução

- `./prompts/grow-from-execution.md`
- `./agents/agentops-growth-architect.md`
- `./rules/growth-artifact-quality.md`
- `./skills/grow-from-execution.md`
- `./prompts/hooks/validate-growth-proposal.md`
- `./governance/lifecycle/artifact-lifecycle-policy.md`

## Erros comuns

- copiar o relatório inteiro
- transformar caso pontual em rule
- criar arquivo sem verificar duplicação

## Checklist rápido

- [ ] O conhecimento é recorrente.
- [ ] A matriz de classificação foi aplicada.
- [ ] O hook validou a proposta.
