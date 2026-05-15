# Problema: criar um novo artefato

## Quando isso acontece

Você identificou um conhecimento novo e não sabe se deve criar arquivo, atualizar arquivo existente ou rejeitar.

## Por que isso importa

Criar arquivo sem responsabilidade clara aumenta complexidade e quebra seleção modular.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: consulte manifesto e lifecycle.
2. Select: escolha o diretório pela responsabilidade.
3. Inject: use governance, rule e skill necessárias antes de alterar.

## Arquivos que normalmente entram na solução

- `./MANIFEST.md`
- `./governance/lifecycle/artifact-lifecycle-policy.md`
- `./governance/authoring/markdown-authoring-standard.md`
- `./governance/quality/artifact-quality-standard.md`
- `./prompts/grow-from-execution.md`
- `./rules/growth-artifact-quality.md`

## Erros comuns

- criar arquivo por preferência estética
- colocar rule dentro de skill
- criar prompt quando o problema é agente ou rule

## Checklist rápido

- [ ] Existe responsabilidade nova e clara.
- [ ] Não há artefato equivalente.
- [ ] O arquivo pode ser selecionado independentemente.
