# Orquestracao de remediacao da auditoria

Este documento inicia o fluxo de orquestracao para as oportunidades e necessidades identificadas na auditoria severa do `agent-ops`.

Este arquivo e documentacao humana de execucao. Ele nao e contexto injetavel por padrao e nao substitui `../MANIFEST.md`, `../governance/` ou os artefatos operacionais aplicaveis.

## Objetivo

Garantir que cada remediacao avance de forma controlada, revisada e rastreavel, sem transformar a auditoria em uma lista solta de melhorias.

Cada item deve passar, nesta ordem, por:

```txt
implementacao do especialista
-> revisor de governanca
-> revisor de documentacao
-> reajustes
-> auditoria coletiva
-> atualizacao das documentacoes
```

## Regra de execucao

- Apenas um item deve ficar em execucao por vez.
- Nenhum item deve pular etapa.
- Nenhum item deve ser marcado como concluido sem evidencia de revisao.
- Mudancas normativas devem citar a fonte primaria afetada.
- Mudancas documentais devem atualizar os roteadores humanos quando necessario.
- Mudancas em prompts, rules, agents, skills ou hooks devem preservar `intake -> find -> select -> inject -> execute`.

## Definicao das etapas

| Etapa | Responsavel sugerido | Entrada obrigatoria | Saida obrigatoria | Criterio de saida |
|---|---|---|---|---|
| Implementacao do especialista | Especialista do tema | Achado, escopo e arquivos provaveis | Alteracao proposta ou implementada | Resolve o problema sem ampliar escopo indevidamente |
| Revisor de governanca | Maintainer de governanca | Diff ou proposta | Parecer PASS, FAIL ou CONDITIONAL | Preserva taxonomia, precedencia, fonte primaria e token economy |
| Revisor de documentacao | Maintainer de docs | Diff ou proposta aprovada em governanca | Parecer documental | README, docs, exemplos ou guias afetados foram atualizados ou declarados como nao aplicaveis |
| Reajustes | Especialista original | Pareceres de revisao | Ajustes aplicados | Todas as pendencias foram resolvidas ou justificadas |
| Auditoria coletiva | Especialista + revisores | Mudanca ajustada | Decisao final | Nao ha bloqueio P0/P1 residual para o item |
| Atualizacao das documentacoes | Maintainer de docs | Decisao final | Documentacao atualizada | Artefatos humanos refletem o estado novo |

## Fila de remediacao

| Ordem | ID | Origem | Necessidade ou oportunidade | Especialista sugerido | Arquivos provaveis | Status inicial |
|---|---|---|---|---|---|---|
| 1 | ORQ-01 | F01 | Criar suite minima de evals e casos de regressao | PromptOps / QA de IA | `evals/`, `docs/examples/` | PASS |
| 2 | ORQ-02 | F04 | Definir guardrails minimos de seguranca operacional | Seguranca de IA | `rules/generation/`, `prompts/hooks/` | PASS |
| 3 | ORQ-03 | F02 | Tornar checkpoints criticos obrigatorios nos fluxos de alto risco | Governanca de agentes | `prompts/hooks/`, `governance/composition/` | PASS |
| 4 | ORQ-04 | F03 | Resolver ausencia ou ambiguidade de `tasks/`, `workflows/` e `policies/` | Arquiteto de informacao | `MANIFEST.md`, `README.md`, `governance/` | PASS |
| 5 | ORQ-05 | F05 | Reforcar contratos dos prompts principais com entradas e saidas obrigatorias | Prompt engineer | `prompts/generation/`, `prompts/review/`, `prompts/planning/`, `prompts/discovery/` | PASS |
| 6 | ORQ-06 | F06, F07 | Consolidar naming e remover contradicoes de severidade | Data governance | `rules/naming/`, `skills/review/`, `prompts/review/` | CONDITIONAL |
| 7 | ORQ-07 | F08 | Reduzir carga de contexto movendo exemplos longos para docs ou evals | Context engineer | `prompts/`, `skills/`, `docs/examples/`, `evals/fixtures/` | CONDITIONAL |
| 8 | ORQ-08 | F09 | Criar templates minimos para novos artefatos | DX / documentacao | `docs/templates/` | PASS |
| 9 | ORQ-09 | F10 | Definir politica objetiva de versionamento e depreciacao | Maintainer | `governance/lifecycle/` | PASS |
| 10 | ORQ-10 | F11 | Padronizar identidade `prompt-ops` versus `agent-ops` | Maintainer de produto | `README.md`, `MANIFEST.md` | PASS |
| 11 | ORQ-11 | F12 | Resolver diretorios vazios nao governados | Maintainer | estrutura raiz local | PASS |
| 12 | ORQ-12 | F12 complementar | Atualizar arvores e roteadores que nao refletem a estrutura real | Documentacao | `README.md`, `MANIFEST.md`, `docs/README.md` | PASS |
| 13 | ORQ-13 | Root index | Criar `INDEX.md` como roteador barato para discovery por LLM | Context engineer | `INDEX.md`, `README.md`, `MANIFEST.md`, `governance/composition/`, `evals/` | PASS |
| 14 | ORQ-14 | Intake Governance | Criar camada barata de triagem antes de discovery | PromptOps / Governanca | `rules/quality/`, `prompts/hooks/`, `skills/orchestration/`, `MANIFEST.md`, `README.md`, `INDEX.md`, `evals/` | PASS |
| 15 | ORQ-15 | Governed Memory | Criar `_memory/` como memoria governada auxiliar e seletiva | Governanca / Context engineer | `_memory/`, `MANIFEST.md`, `README.md`, `INDEX.md`, `governance/composition/`, `evals/` | PASS |
| 16 | ORQ-16 | Artifact Synchronization | Criar registry e policy leve de sync targets | Governanca / Lifecycle | `governance/authoring/`, `governance/lifecycle/`, `MANIFEST.md`, `README.md`, `INDEX.md`, `evals/` | PASS |
| 17 | ORQ-17 | Small Model Execution Mode | Limitar modelos pequenos a execucao bounded e escalacao de governanca | Context engineer / Governanca | `INDEX.md`, `README.md`, `governance/composition/`, `evals/` | PASS |
| 18 | ORQ-18 | Delegation Governance | Dimensionar tarefas grandes, decompor e delegar mantendo veredito no orquestrador | Orquestracao / Governanca | `prompts/hooks/`, `rules/architecture/`, `skills/orchestration/`, `governance/composition/`, `evals/` | PASS |

## Registro de passagem por gates

Use esta tabela para controlar a execucao. Cada celula deve receber `PENDING`, `PASS`, `FAIL`, `CONDITIONAL` ou `N/A`, sempre com evidencia no registro do item.

| ID | Implementacao do especialista | Revisor de governanca | Revisor de documentacao | Reajustes | Auditoria coletiva | Atualizacao das documentacoes |
|---|---|---|---|---|---|---|
| ORQ-01 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-02 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-03 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-04 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-05 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-06 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-07 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-08 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-09 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-10 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-11 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-12 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-13 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-14 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-15 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-16 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-17 | PASS | PASS | PASS | PASS | PASS | PASS |
| ORQ-18 | PASS | PASS | PASS | PASS | PASS | PASS |

## Contrato de registro por item

Cada item deve manter um registro no seguinte formato antes de avancar para a etapa seguinte:

```txt
ID:
Etapa atual:
Responsavel:
Escopo:
Arquivos avaliados:
Arquivos alterados:
Evidencia:
Riscos:
Pendencias:
Decisao: PASS | FAIL | CONDITIONAL
Proxima etapa:
```

## Registro por item desta feature

```txt
ID: ORQ-13
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / Context engineer
Escopo: Criar e governar INDEX.md como roteador barato de discovery inicial por LLM.
Arquivos avaliados: INDEX.md, README.md, MANIFEST.md, governance/composition/context-composition.md, evals/manual-regression-suite.md
Arquivos alterados: INDEX.md, README.md, MANIFEST.md, governance/composition/context-composition.md, evals/manual-regression-suite.md, evals/index-feature-results.md
Evidencia: INDEX.md existe, tem menos de 120 linhas, referencia apenas caminhos existentes e esta registrado em manifesto, composicao e evals.
Riscos: INDEX.md virar fonte normativa ou contexto carregado por habito.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Manter sincronizado apenas quando roteadores raiz mudarem.
```

```txt
ID: ORQ-14
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / PromptOps
Escopo: Implementar Intake Governance como camada barata antes de find.
Arquivos avaliados: docs/remediation/intake-governance-spec.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, rules/quality/README.md, prompts/hooks/README.md, skills/orchestration/README.md, evals/manual-regression-suite.md
Arquivos alterados: rules/quality/user-input-quality.md, prompts/hooks/validate-user-intent.md, skills/orchestration/intake-governance.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, rules/README.md, rules/quality/README.md, prompts/README.md, prompts/hooks/README.md, skills/README.md, skills/orchestration/README.md, evals/manual-regression-suite.md, evals/intake-governance-results.md, evals/README.md
Evidencia: fluxo oficial atualizado para intake -> find -> select -> inject -> execute; rule/hook/skill criados; EVAL-012 registrado com PASS.
Riscos: intake virar burocracia ou ser usado para carregar contexto antes de find.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Executar regressao manual quando prompts de entrada forem alterados.
```

```txt
ID: ORQ-15
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / Context engineer
Escopo: Implementar Governed Memory como contexto auxiliar, seletivo e auditavel em `_memory/`.
Arquivos avaliados: docs/remediation/governed-memory-spec.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, evals/manual-regression-suite.md
Arquivos alterados: _memory/README.md, _memory/project-decisions.md, _memory/stable-preferences.md, _memory/lessons-learned.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, evals/manual-regression-suite.md, evals/governed-memory-results.md, evals/README.md
Evidencia: `_memory/` criado com tres memories aprovadas, fonte rastreavel, limites explicitos e EVAL-013 registrado com PASS.
Riscos: memory virar fonte normativa, historico bruto ou contexto carregado por padrao.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Revisar memories em 2026-08-24 ou quando fonte primaria mudar.
```

```txt
ID: ORQ-16
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / Governanca de lifecycle
Escopo: Implementar Artifact Synchronization com registry central leve e policy de impacto.
Arquivos avaliados: docs/remediation/artifact-synchronization-spec.md, governance/authoring/README.md, governance/lifecycle/README.md, MANIFEST.md, README.md, INDEX.md, evals/manual-regression-suite.md
Arquivos alterados: governance/authoring/artifact-registry.md, governance/lifecycle/artifact-synchronization-policy.md, governance/authoring/README.md, governance/lifecycle/README.md, governance/lifecycle/artifact-lifecycle-policy.md, MANIFEST.md, README.md, INDEX.md, evals/manual-regression-suite.md, evals/artifact-synchronization-results.md, evals/README.md
Evidencia: registry criado com sync targets; policy criada com classes de impacto; EVAL-014 registrado com PASS.
Riscos: registry virar catalogo total ou metadata inline virar custo recorrente.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Revisar registry trimestralmente e quando artefato critico mudar.
```

```txt
ID: ORQ-17
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / Governanca
Escopo: Implementar Small Model Execution Mode como modo barato para execucao delimitada por modelos pequenos.
Arquivos avaliados: docs/remediation/small-model-execution-mode-spec.md, INDEX.md, README.md, governance/composition/context-composition.md, evals/manual-regression-suite.md
Arquivos alterados: INDEX.md, README.md, governance/composition/context-composition.md, evals/manual-regression-suite.md, evals/small-model-execution-results.md, evals/README.md, docs/remediation/audit-remediation-orchestration.md, governance/authoring/artifact-registry.md
Evidencia: INDEX e context-composition limitam contexto para modelos pequenos; formato BLOCKED_OR_ESCALATE definido; EVAL-015 e evals/small-model-execution-results.md registrados com PASS; registry e sync targets revisados.
Riscos: modelo pequeno tentar governar ou carregar metagovernanca demais.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Reavaliar quando novos modos de execucao ou modelos forem adicionados.
```

```txt
ID: ORQ-18
Etapa atual: Atualizacao das documentacoes
Responsavel: Orquestrador / Governanca
Escopo: Implementar Delegation Governance como camada de sizing, decomposicao e orquestracao para tarefas grandes.
Arquivos avaliados: docs/remediation/delegation-governance-spec.md, docs/remediation/README.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, prompts/hooks/README.md, rules/architecture/README.md, skills/orchestration/README.md, evals/manual-regression-suite.md
Arquivos alterados: prompts/hooks/size-task-for-delegation.md, rules/architecture/delegation-boundaries.md, skills/orchestration/task-decomposition-orchestration.md, MANIFEST.md, README.md, INDEX.md, governance/composition/context-composition.md, prompts/README.md, prompts/hooks/README.md, rules/README.md, rules/architecture/README.md, skills/README.md, skills/orchestration/README.md, evals/manual-regression-suite.md, evals/delegation-governance-results.md, evals/README.md, docs/remediation/README.md, docs/remediation/audit-remediation-orchestration.md, governance/authoring/artifact-registry.md
Evidencia: hook de sizing criado; rule de limites criada; skill de orquestracao criada; context-composition reconhece sizing e delegacao; EVAL-016 registrado com PASS.
Riscos: delegacao virar custo automatico, subagente ampliar escopo ou orquestrador terceirizar veredito.
Pendencias: Nenhuma bloqueante.
Decisao: PASS
Proxima etapa: Reavaliar quando forem adicionados novos modos de execucao multiagente.
```

## Registro consolidado desta execucao

### Itens aprovados

- ORQ-01: criado `../../evals/` com suite manual de regressao.
- ORQ-02: criado `../../rules/generation/operational-safety-guardrails.md`.
- ORQ-03: criado `../../prompts/hooks/validate-operational-safety.md` e regra de checkpoint obrigatorio por risco.
- ORQ-04: `tasks/`, `workflows/` e `policies/` definidos como nao oficiais em v0.1.
- ORQ-05: prompts principais reforcados com `MUST` e entradas/saidas minimas.
- ORQ-08: criado template humano unico em `../templates/new-artifact.md`.
- ORQ-09: lifecycle recebeu status e regra minima de depreciacao.
- ORQ-10: identidade oficial `agent-ops` explicitada.
- ORQ-11: diretorios vazios nao oficiais foram removidos da raiz local.
- ORQ-12: `../../README.md` reescrito como mapa humano do sistema e workflows.
- ORQ-13: criado `../../INDEX.md` como roteador barato de discovery inicial por LLM e registrado em manifesto, composicao e evals.
- ORQ-14: criado Intake Governance com `../../rules/quality/user-input-quality.md`, `../../prompts/hooks/validate-user-intent.md` e `../../skills/orchestration/intake-governance.md`.
- ORQ-15: criado `../../_memory/` como memoria governada auxiliar, seletiva e fora da composicao padrao.
- ORQ-16: criado `../../governance/authoring/artifact-registry.md` e `../../governance/lifecycle/artifact-synchronization-policy.md`.
- ORQ-17: criado Small Model Execution Mode para execucao bounded por modelos pequenos com escalacao obrigatoria de governanca.
- ORQ-18: criado Delegation Governance com sizing, limites de delegacao e orquestracao com veredito final do orquestrador.

### Itens fechados nesta execucao

- ORQ-06: naming foi consolidado; `reference-severity.md` permanece fonte primaria de severidade, `reference-units.md` permanece fonte primaria de unidades e `rule-08-foreign-keys.md` foi alinhada a `CRITICAL`.
- ORQ-07: prompts e skills de naming foram compactados; exemplos completos foram movidos para `../../docs/examples/semantic-naming-examples.md`; suite manual foi registrada em `../../evals/v0.1-manual-results.md`.

### Veredito do orquestrador

Status geral: PASS.

Liberado para tag v0.1 como base de governanca operacional para piloto profissional controlado.

Restricao: producao critica ainda requer execucao real dos controles de plataforma fora deste repositorio.
