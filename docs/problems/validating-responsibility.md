# Problema: validar responsabilidade de um artefato

## Quando isso acontece

Você criou ou revisou um `.md` e quer saber se ele está no lugar certo.

## Por que isso importa

Responsabilidade misturada quebra SOLID em Markdown e torna a composição imprevisível.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: identifique tipo, finalidade e limites.
2. Select: compare com a responsabilidade do diretório.
3. Inject: use governance de autoria e qualidade para revisar.

## Arquivos que normalmente entram na solução

- `./MANIFEST.md`
- `./governance/principles/core-principles.md`
- `./governance/authoring/markdown-authoring-standard.md`
- `./governance/quality/artifact-quality-standard.md`
- `./governance/lifecycle/artifact-lifecycle-policy.md`

## Erros comuns

- misturar prompt com rule
- colocar procedimento dentro de agent
- usar governance para regra técnica de output

## Checklist rápido

- [ ] O arquivo tem uma responsabilidade principal.
- [ ] O tipo observado combina com o diretório.
- [ ] Dependências estão explícitas por caminho.
