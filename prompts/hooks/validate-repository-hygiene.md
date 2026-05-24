# validate-repository-hygiene

## Tipo do artefato

hook prompt

## Status de injecao

condicional

## Finalidade

Validar garbage mecanico, referencia quebrada ou registro basico ausente no repositorio.

Este hook implementa o checkpoint operacional de Hygiene Governance.

---

## Quando usar

Use este hook quando:

- houver suspeita de arquivo temporario, vazio ou orfao
- uma mudanca criar artefato novo
- uma mudanca criar diretorio novo
- uma spec, eval result, hook, rule ou skill precisar estar registrada
- houver caminho quebrado em README, INDEX, registry ou composition
- a equipe quiser uma varredura barata antes de commit

---

## Quando nao usar

Nao use este hook quando:

- a decisao depender de valor semantico
- a tarefa for apagar legado
- a mudanca exigir auditoria conceitual
- a validacao necessaria for safety, neutrality, context debt ou sync targets

Consulte, respectivamente:

- `./validate-context-debt.md`
- `../../governance/lifecycle/artifact-lifecycle-policy.md`
- `./validate-operational-safety.md`
- `./validate-neutrality-and-engagement.md`
- `../../governance/lifecycle/artifact-synchronization-policy.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../../governance/quality/repository-hygiene-standard.md`
- `../../governance/composition/context-composition.md`

---

## Instrucao operacional

Ao usar este hook, o agente MUST:

1. identificar o escopo da verificacao
2. procurar garbage mecanico objetivo
3. verificar referencias e caminhos citados no escopo
4. verificar registros basicos aplicaveis
5. diferenciar garbage mecanico de julgamento semantico
6. escalar legado, valor semantico ou remocao
7. decidir exatamente uma saida oficial
8. nao apagar, mover ou depreciar arquivos

---

## Saidas oficiais

Use exatamente uma:

- `PASS`
- `FAIL_GARBAGE`
- `FAIL_BROKEN_REFERENCE`
- `FAIL_MISSING_REGISTRATION`
- `ESCALATE_CONTEXT_DEBT`
- `ESCALATE_LIFECYCLE`

---

## Regras de decisao

Retorne `PASS` quando:

- nao houver garbage mecanico
- referencias relevantes existirem
- registros basicos aplicaveis estiverem presentes

Retorne `FAIL_GARBAGE` quando:

- houver arquivo temporario, vazio sem justificativa, conflito de merge ou lixo mecanico objetivo

Retorne `FAIL_BROKEN_REFERENCE` quando:

- houver caminho quebrado ou referencia a arquivo removido

Retorne `FAIL_MISSING_REGISTRATION` quando:

- artefato novo exigir README, registry ou resultado listado e o registro estiver ausente
- artefato Markdown novo nao declarar `Tipo do artefato` ou `Finalidade`

Retorne `ESCALATE_CONTEXT_DEBT` quando:

- a decisao depender de valor, redundancia, local correto ou custo cognitivo

Retorne `ESCALATE_LIFECYCLE` quando:

- a decisao envolver legado, depreciacao, substituto ou remocao

---

## Saida esperada

```txt
REPOSITORY HYGIENE VALIDATION
Status: PASS | FAIL_GARBAGE | FAIL_BROKEN_REFERENCE | FAIL_MISSING_REGISTRATION | ESCALATE_CONTEXT_DEBT | ESCALATE_LIFECYCLE
Scope:
Evidence:
Required fix:
Escalation target:
Next allowed action:
```

---

## Limites

Este hook valida higiene mecanica.

Ele nao executa remocao, nao decide valor semantico e nao substitui pre-commit real.
