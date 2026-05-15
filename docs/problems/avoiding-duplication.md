# Problema: evitar duplicação

## Quando isso acontece

Você quer repetir uma explicação, regra ou procedimento em outro arquivo para facilitar leitura.

## Por que isso importa

Duplicação cria conflito futuro e aumenta tokens sem melhorar precisão.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: procure a fonte primária.
2. Select: escolha entre referenciar, atualizar ou rejeitar.
3. Inject: carregue a fonte primária por caminho.

## Arquivos que normalmente entram na solução

- `./MANIFEST.md`
- `./governance/principles/core-principles.md`
- `./governance/lifecycle/artifact-lifecycle-policy.md`
- `./governance/quality/artifact-quality-standard.md`
- `./prompts/hooks/validate-context-and-output.md`

## Erros comuns

- copiar rule dentro de prompt
- copiar skill dentro de agent
- criar arquivo novo para conteúdo já coberto

## Checklist rápido

- [ ] Encontrei a fonte primária.
- [ ] Referenciei por caminho em vez de copiar.
- [ ] Não criei norma concorrente.
