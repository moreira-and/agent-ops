# intake-governance

## Tipo do artefato

skill

## Finalidade

Definir o procedimento reutilizavel para triagem de pedidos humanos antes de `find -> select -> inject -> execute`.

Esta skill ajuda o agente a aplicar Intake Governance sem transformar toda tarefa simples em processo pesado.

---

## Quando usar

Use esta skill quando precisar:

- decompor um pedido humano em intencao, escopo, risco e criterio de sucesso
- decidir se deve executar, perguntar, pedir aprovacao ou recusar
- manter baixo custo antes da descoberta de contexto
- orientar uso de `../../prompts/hooks/validate-user-intent.md`
- evitar que falta de bom senso na ponta vire execucao insegura

---

## Quando nao usar

Nao use esta skill como fonte primaria para:

- norma de qualidade da entrada humana
- prompt de checkpoint
- regra de seguranca operacional detalhada
- composicao de contexto

Consulte, respectivamente:

- `../../rules/quality/user-input-quality.md`
- `../../prompts/hooks/validate-user-intent.md`
- `../../rules/generation/operational-safety-guardrails.md`
- `../../governance/composition/context-composition.md`

---

## Dependencias relacionadas

- `../../rules/quality/user-input-quality.md`
- `../../prompts/hooks/validate-user-intent.md`
- `../../governance/composition/context-composition.md`

---

## Procedimento

### 1. Ler o pedido original

Comece pelo pedido humano como fonte da intencao.

Nao carregue diretorios, docs, evals ou skills adicionais antes de entender se o pedido pode seguir para discovery.

### 2. Extrair a intencao

Identifique:

- objetivo declarado
- objeto ou alvo da tarefa
- resultado esperado
- restricoes explicitas
- termos vagos que podem esconder risco

### 3. Classificar risco

Classifique o risco como:

| Risco | Criterio |
|---|---|
| `low` | leitura, explicacao, mudanca pequena, reversivel ou sem efeito externo |
| `medium` | alteracao tecnica localizada, ambiguidade moderada ou impacto limitado |
| `high` | destruicao, escrita ampla, dado sensivel, credencial, decisao critica ou efeito externo |

### 4. Decidir a saida de intake

Use a fonte primaria:

- `../../rules/quality/user-input-quality.md`

Saidas permitidas:

- `READY_TO_FIND`
- `NEEDS_CLARIFICATION`
- `NEEDS_APPROVAL`
- `REFUSE_OR_REDIRECT`

### 5. Manter baixo atrito

Se o pedido for claro, baixo risco e reversivel, siga para `find`.

Nao faca perguntas apenas para obter perfeicao. Pergunte somente quando a resposta mudar a seguranca, o escopo ou o resultado da execucao.

### 6. Perguntar com precisao

Quando precisar de esclarecimento, faca no maximo tres perguntas.

Cada pergunta deve remover uma lacuna bloqueante.

### 7. Exigir aprovacao quando necessario

Para risco alto, nao transforme silencio em consentimento.

Solicite aprovacao explicita antes de prosseguir.

### 8. Encaminhar para discovery

Quando a saida for `READY_TO_FIND`, siga para:

```txt
find -> select -> inject -> execute
```

Selecione contexto conforme:

- `../../governance/composition/context-composition.md`

---

## Saida recomendada

```txt
INTAKE DECISION
Status: READY_TO_FIND | NEEDS_CLARIFICATION | NEEDS_APPROVAL | REFUSE_OR_REDIRECT
Reason:
Risk:
Missing context:
Questions:
Next step:
```

---

## Limites

Esta skill descreve procedimento de triagem.

Ela nao substitui a rule `../../rules/quality/user-input-quality.md`.

Ela nao substitui o hook `../../prompts/hooks/validate-user-intent.md`.

Ela nao executa a tarefa final.
