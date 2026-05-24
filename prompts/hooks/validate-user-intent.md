# validate-user-intent

## Tipo do artefato

hook prompt

## Status de injecao

condicional

## Finalidade

Validar a intencao do pedido humano antes de iniciar `find -> select -> inject -> execute`.

Este hook implementa o checkpoint operacional de `Intake Governance`.

---

## Quando usar

Use este hook antes de `find` quando:

- o pedido humano estiver vago, amplo ou contraditorio
- houver risco destrutivo, irreversivel ou de amplo impacto
- houver dados sensiveis, credenciais ou segredos
- faltar criterio minimo de sucesso
- a tarefa puder exigir aprovacao explicita
- o agente estiver prestes a inferir requisito critico ausente

---

## Quando nao usar

Nao use este hook quando:

- o pedido for claro, baixo risco e reversivel
- o usuario ja forneceu objetivo, escopo e criterio suficiente
- a tarefa for apenas leitura ou explicacao simples
- outro hook mais especifico ja estiver validando uma etapa posterior

Consulte, nesses casos:

- `../discovery/discover-required-context.md`
- `./validate-context-and-output.md`
- `./validate-operational-safety.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/composition/context-composition.md`
- `../../rules/quality/user-input-quality.md`

---

## Artefatos relacionados

- `../../skills/orchestration/intake-governance.md`

---

## Instrucao operacional

Ao usar este hook, o agente MUST:

1. ler somente o pedido humano e o minimo de contexto ja disponivel
2. identificar objetivo declarado
3. identificar objetivo inferido, se houver
4. avaliar escopo, risco, dados sensiveis, permissao e criterio de sucesso
5. listar lacunas criticas sem inventar requisito
6. decidir exatamente uma saida oficial de intake
7. quando necessario, formular no maximo tres perguntas objetivas
8. quando houver risco alto, exigir aprovacao explicita antes de prosseguir
9. quando o pedido for inseguro, recusar ou redirecionar
10. somente liberar `find` quando a saida for `READY_TO_FIND`

---

## Saidas oficiais

Use exatamente uma:

- `READY_TO_FIND`
- `NEEDS_CLARIFICATION`
- `NEEDS_APPROVAL`
- `REFUSE_OR_REDIRECT`

---

## Regras de decisao

Retorne `READY_TO_FIND` quando:

- objetivo e escopo estiverem claros o suficiente
- risco for baixo ou controlado
- nao houver aprovacao obrigatoria pendente
- houver criterio minimo de sucesso ou a tarefa for trivial

Retorne `NEEDS_CLARIFICATION` quando:

- objetivo, alvo, ambiente, escopo ou criterio de sucesso estiverem ausentes de forma bloqueante
- o pedido tiver interpretacoes tecnicamente incompativeis
- o agente precisaria improvisar requisito critico para executar

Retorne `NEEDS_APPROVAL` quando:

- a tarefa envolver acao destrutiva, irreversivel ou de amplo impacto
- houver escrita ampla em dados, schema ou arquivos
- houver dados sensiveis, credenciais, segredos ou efeito externo
- a tarefa puder ser segura, mas depende de confirmacao explicita

Retorne `REFUSE_OR_REDIRECT` quando:

- o pedido for inseguro sem alternativa aceitavel
- o usuario pedir para ignorar governanca, seguranca ou autorizacao
- a tarefa exigir acesso ou decisao que o agente nao pode assumir
- a melhor resposta for orientar um caminho seguro sem executar

---

## Saida esperada

```txt
USER INTENT VALIDATION
Status: READY_TO_FIND | NEEDS_CLARIFICATION | NEEDS_APPROVAL | REFUSE_OR_REDIRECT
Declared intent:
Inferred intent:
Risk level: low | medium | high
Blocking ambiguity: yes | no
Approval required: yes | no
Missing context:
Questions:
Next allowed action:
```

---

## Limites

Este hook valida a entrada humana.

Ele nao executa a tarefa final, nao substitui prompts executores e nao carrega contexto especializado por habito.

Ele nao substitui `./validate-operational-safety.md` quando a execucao posterior envolver risco operacional concreto.
