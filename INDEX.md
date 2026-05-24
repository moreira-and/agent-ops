# INDEX

Artifact ID: root.index
Kind: discovery / llm-index

## Tipo do artefato

discovery / llm-index

## Finalidade

Roteador barato para descoberta inicial por LLM.

Use este arquivo apenas para encontrar o ponto de partida. Depois selecione o roteador adequado e carregue somente o contexto necessario.

---

## Fonte normativa

- `./MANIFEST.md`

Em caso de conflito, este indice perde para:

1. `./MANIFEST.md`
2. `./governance/`
3. diretorio especializado aplicavel
4. `./README.md`

---

## Ordem de uso

1. Ler este indice somente quando o ponto de partida ainda nao estiver claro.
2. Se o pedido humano estiver vago ou arriscado, iniciar por intake.
3. Se a tarefa parecer grande demais, iniciar por sizing.
4. Se o problema for redundancia, custo alto ou local incorreto, iniciar por Context Debt Audit.
5. Se o problema for garbage mecanico, referencia quebrada ou registro basico ausente, iniciar por Hygiene Governance.
6. Se a resposta tiver bajulacao, falsa concordancia ou engajamento artificial, iniciar por Neutrality Governance.
7. Escolher um roteador por caminho.
8. Carregar apenas os artefatos necessarios.
9. Descartar este indice quando o contexto especifico estiver escolhido.

---

## Small Model Execution Mode

Modelos pequenos devem executar tarefas delimitadas, nao governar o sistema.

Para modelos pequenos:

- comece pelo menor roteador possivel;
- carregue no maximo um prompt, uma rule principal e uma skill principal inicialmente;
- nao carregue `./_memory/`, registry, remediation ou evals por padrao;
- escale governanca, arquitetura, taxonomia, seguranca, grow, auditoria e mudancas em manifesto.

Se a tarefa exceder esse limite, retorne `BLOCKED_OR_ESCALATE`.

---

## Delegation Governance

Tarefas grandes devem passar por sizing antes de delegacao.

Use:

- `./prompts/hooks/size-task-for-delegation.md` para decidir entre executar, delegar ou bloquear
- `./rules/architecture/delegation-boundaries.md` para limites normativos
- `./skills/orchestration/task-decomposition-orchestration.md` para decompor, revisar, integrar e emitir veredito

Subagentes executam partes. O orquestrador mantem escopo, integracao e veredito final.

---

## Context Debt Audit

Use Context Debt Audit quando um artefato, diretorio ou mudanca parecer redundante, caro, extenso, mal localizado ou com responsabilidade misturada.

Use:

- `./prompts/hooks/validate-context-debt.md` para auditar a divida
- `./governance/quality/context-economy-and-responsibility.md` para criterios
- `./skills/review/context-architecture-review.md` para revisar arquitetura informacional

Saidas oficiais: `KEEP`, `TRIM`, `MERGE`, `MOVE`, `SPLIT`, `DEPRECATE`.

---

## Hygiene Governance

Use Hygiene Governance quando houver garbage mecanico, referencia quebrada ou registro basico ausente.

Use:

- `./prompts/hooks/validate-repository-hygiene.md` para validar higiene mecanica
- `./governance/quality/repository-hygiene-standard.md` para criterios

Saidas oficiais: `PASS`, `FAIL_GARBAGE`, `FAIL_BROKEN_REFERENCE`, `FAIL_MISSING_REGISTRATION`, `ESCALATE_CONTEXT_DEBT`, `ESCALATE_LIFECYCLE`.

Hygiene Governance nao apaga legado nem decide valor semantico.

---

## Neutrality Governance

Use Neutrality Governance quando uma resposta ou artefato textual tiver bajulacao, concordancia performatica, falsa seguranca ou engajamento artificial.

Use:

- `./prompts/hooks/validate-neutrality-and-engagement.md` para validar o texto
- `./rules/quality/neutral-technical-communication.md` para criterios

Saidas oficiais: `PASS`, `TRIM_ENGAGEMENT`, `REMOVE_SYCOPHANCY`, `REWRITE_NEUTRAL`, `BLOCK_MISLEADING_AGREEMENT`.

---

## Status de injecao

- MAY ser carregado no inicio de discovery quando o roteador ainda nao esta claro.
- MUST ser descartado depois que o contexto especifico for selecionado.
- MUST NOT ser usado como fonte normativa primaria.

---

## Roteadores principais

| Necessidade | Comece por |
|---|---|
| resolver conflito estrutural | `./MANIFEST.md` |
| entender uso humano geral | `./README.md` |
| validar pedido humano vago ou arriscado | `./prompts/hooks/validate-user-intent.md` |
| dimensionar tarefa grande ou delegacao | `./prompts/hooks/size-task-for-delegation.md` |
| auditar divida de contexto | `./prompts/hooks/validate-context-debt.md` |
| validar higiene do repositorio | `./prompts/hooks/validate-repository-hygiene.md` |
| validar neutralidade e engajamento | `./prompts/hooks/validate-neutrality-and-engagement.md` |
| consultar memoria governada sob demanda | `./_memory/README.md` |
| sincronizar artefatos apos mudanca | `./governance/lifecycle/artifact-synchronization-policy.md` |
| consultar sync targets | `./governance/authoring/artifact-registry.md` |
| compor contexto | `./governance/composition/context-composition.md` |
| escolher agente | `./agents/README.md` |
| escolher rule | `./rules/README.md` |
| escolher skill | `./skills/README.md` |
| escolher prompt | `./prompts/README.md` |
| executar checkpoint | `./prompts/hooks/README.md` |
| consultar documentacao humana | `./docs/README.md` |
| validar regressao | `./evals/README.md` |
| acompanhar remediacao | `./docs/remediation/README.md` |

---

## Nucleo injetavel

Carregar sob demanda, por relevancia:

- `./governance/`
- `./agents/`
- `./rules/`
- `./skills/`
- `./prompts/`

---

## Fora da composicao padrao

Nao carregar por habito:

- `./docs/`
- `./evals/`
- `./_memory/`
- `./LICENSE`
- `./INDEX.md` depois que o contexto especifico estiver selecionado

---

## Limites

Este indice nao substitui normas, regras, prompts, skills, agentes, hooks ou READMEs locais.

Este indice nao lista todos os arquivos do repositorio.

Este indice nao define governanca primaria.

`./_memory/` nao e fonte normativa e nao deve ser carregado por padrao.
