# validate-growth-proposal

## Tipo do artefato

hook prompt

## Status de injeção

condicional

## Finalidade

Validar se uma proposta de grow respeita governança, responsabilidade única, token economy e ausência de duplicação.

---

## Quando usar

Use este hook quando precisar:

- revisar proposta de criação ou atualização por grow
- validar classificação de conhecimento
- bloquear absorção bruta de execução
- checar duplicação antes de alterar artefatos
- validar mudanças após implementação

---

## Quando não usar

Não use este hook para:

- executar o fluxo completo de grow
- definir procedimento de destilação
- criar artefatos diretamente
- registrar histórico humano

Consulte, respectivamente:

- `../grow-from-execution.md`
- `../../skills/grow-from-execution.md`
- `../../agents/agentops-growth-architect.md`
- `../../docs/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/principles/core-principles.md`
- `../../governance/composition/context-composition.md`
- `../../governance/lifecycle/artifact-lifecycle-policy.md`
- `../../governance/quality/artifact-quality-standard.md`
- `../../rules/growth-artifact-quality.md`

---

## Precedência

Este hook valida proposta ou resultado.

Ele não substitui prompt, governance, agent, rules ou skill.

---

## Momento de uso

Este hook SHOULD ser acionado:

- depois da proposta de grow
- antes de alterar arquivos
- depois da implementação, quando houver mudança

---

## Checklist de validação

Validar:

- [ ] há arquivo `.md` de execução como evidência
- [ ] conhecimento bruto não foi copiado
- [ ] cada candidato tem classificação correta
- [ ] cada artefato tem responsabilidade única
- [ ] dependências estão declaradas por caminho
- [ ] artefato equivalente foi verificado
- [ ] não há duplicação conceitual relevante
- [ ] token economy melhora ou não piora a composição padrão
- [ ] `find -> select -> inject` foi preservado
- [ ] ordem `prompt -> governance -> agent -> rules -> skills` foi respeitada
- [ ] `../../docs/` não virou fonte normativa
- [ ] `../../evals/` não virou fonte normativa
- [ ] proposta é genérica para qualquer modelo de IA

---

## Critérios de aprovação

A proposta é aprovada quando:

- todo conhecimento aceito tem evidência
- a classificação está correta
- não há duplicação relevante
- os artefatos são plugáveis
- a precedência normativa foi preservada
- a mudança reduz ambiguidade ou melhora recuperação

---

## Critérios de reprovação

A proposta deve ser reprovada quando:

- copiar conteúdo bruto de execução
- criar regra global sem recorrência
- duplicar fonte primária existente
- misturar prompt, agent, rule, skill, hook ou governance
- exigir leitura indiscriminada do repositório
- depender de vendor, modelo ou framework específico
- transformar `../../docs/` em contexto injetável padrão
- transformar `../../evals/` em contexto injetável padrão

---

## Saída esperada

O hook SHOULD produzir:

```txt
GROW VALIDATION RESULT
Status: PASS | FAIL | CONDITIONAL
Evidence checked: yes | no
Classification issues: <list>
Duplication issues: <list>
Token economy impact: improves | neutral | worsens
Recommendation: APPROVE | BLOCK | REQUIRES_REVIEW
```

---

## Limites

Este hook valida conformidade de grow.

Este hook não executa destilação, classificação completa ou implementação.
