# Exemplo: grow a partir de execução

Este exemplo mostra o fluxo humano para usar grow sem transformar execução passada em memória bruta.

## Situação

Entrada: um `.md` de execução com auditoria, correções aplicadas e aprendizados.

## Composição

```txt
prompt:
- ./prompts/grow-from-execution.md

governance:
- ./governance/principles/core-principles.md
- ./governance/composition/context-composition.md
- ./governance/lifecycle/artifact-lifecycle-policy.md
- ./governance/quality/artifact-quality-standard.md

agent:
- ./agents/agentops-growth-architect.md

rules:
- ./rules/growth-artifact-quality.md

skills:
- ./skills/grow-from-execution.md

hook:
- ./prompts/hooks/validate-growth-proposal.md
```

## Como aplicar

1. Informe o caminho do `.md` de execução.
2. Peça extração de conhecimento reutilizável.
3. Peça classificação: prompt, agent, rule, skill, hook, governance, docs ou rejeição.
4. Peça plano antes de alterar arquivos.
5. Valide com o hook.

## Erros a evitar

- copiar o relatório inteiro
- criar rule sem recorrência
- ignorar artefatos existentes
