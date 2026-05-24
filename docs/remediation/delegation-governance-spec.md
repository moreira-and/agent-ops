# Spec: Delegation Governance

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir a governanca para tarefas grandes demais para execucao direta por um unico agente.

Regra central:

```txt
Subagentes podem executar partes; o orquestrador mantem escopo, integracao e veredito final.
```

---

## Problema

Algumas tarefas no `agent-ops` ficam grandes demais para uma unica execucao segura.

Quando isso acontece sem governanca, o agente tende a:

- carregar contexto demais;
- misturar planejamento, implementacao e revisao;
- improvisar escopo;
- perder rastreabilidade;
- delegar sem contrato claro;
- aceitar achados de subagentes sem julgamento;
- produzir veredito fraco ou contraditorio.

Isso fere a filosofia do repositorio: baixa carga cognitiva, governanca real, simplicidade operacional e responsabilidade explicita.

---

## Objetivo

Criar `Delegation Governance` para:

- identificar quando uma tarefa e grande demais;
- quebrar o trabalho em partes pequenas e independentes;
- delegar apenas o que tiver contrato claro;
- manter subagentes em escopos limitados;
- impedir delegacao de veredito;
- preservar `intake -> find -> select -> inject -> execute`;
- reduzir custo de contexto;
- melhorar qualidade sem criar burocracia permanente.

---

## Nao objetivos

Nao fazer nesta feature:

- criar runtime multiagente;
- criar framework de agentes;
- obrigar uso de subagentes em toda tarefa;
- permitir que subagente decida governanca final;
- substituir review humano em producao critica;
- criar diretorio novo sem necessidade;
- transformar o repositorio em plataforma de swarm;
- duplicar regras ja existentes de composicao, safety ou lifecycle.

---

## Definicao

`Delegation Governance` e o dominio que regula quando e como uma tarefa pode ser quebrada e delegada.

Ele tem tres capacidades:

| Capacidade | Funcao |
|---|---|
| Task Sizing | decidir se a tarefa cabe em execucao direta |
| Task Decomposition | quebrar tarefa grande em subtarefas com escopo claro |
| Orchestrated Delegation | delegar, revisar, integrar e emitir veredito final |

---

## Posicao no fluxo

Fluxo padrao:

```txt
intake -> find -> select -> inject -> execute
```

Fluxo com sizing:

```txt
intake -> sizing -> find -> select -> inject -> execute
```

Fluxo quando a tarefa for grande:

```txt
intake
-> sizing
-> decompose
-> delegate
-> review
-> integrate
-> verdict
```

`sizing` nao substitui intake. Intake valida a qualidade e risco do pedido humano. Sizing decide se a execucao direta e adequada.

---

## Quando usar delegacao

Delegacao MAY ser usada quando a tarefa:

- envolve muitos arquivos ou dominios;
- exige auditoria ampla;
- mistura implementacao, documentacao e validacao;
- pode ser quebrada em partes independentes;
- tem subtarefas com artefatos de entrada e saida claros;
- se beneficiaria de revisao paralela;
- excede contexto pratico para uma unica execucao.

Delegacao SHOULD ser usada quando:

- ha risco de perder coerencia por excesso de escopo;
- ha revisoes independentes que podem detectar falhas;
- a tarefa pede explicitamente uso de subagentes;
- o orquestrador precisa preservar veredito sem executar tudo sozinho.

---

## Quando nao usar delegacao

Delegacao MUST NOT ser usada quando:

- a tarefa e simples e direta;
- o custo de coordenar subagentes supera o ganho;
- o subagente precisaria decidir governanca final;
- a subtarefa nao tem entrada e saida verificaveis;
- varios subagentes editariam o mesmo arquivo sem necessidade;
- a tarefa envolve segredo, credencial ou dado sensivel sem politica especifica;
- a delegacao serviria apenas para terceirizar responsabilidade.

---

## Criterios de task sizing

Uma tarefa deve ser considerada grande quando atender dois ou mais criterios:

- toca mais de um dominio operacional;
- altera mais de tres grupos de artefatos;
- exige implementacao e revisao independente;
- exige auditoria coletiva;
- possui risco P0/P1;
- contem ambiguidade que precisa ser resolvida por decomposicao;
- pode exceder a janela de contexto util;
- mistura governanca, documentacao, evals e execucao.

Uma tarefa deve permanecer direta quando:

- altera um unico arquivo ou artefato;
- tem criterio de aceite local;
- nao muda governanca;
- nao exige julgamento independente;
- pode ser validada com leitura pequena.

---

## Contrato de decomposicao

Toda subtarefa delegada MUST declarar:

```txt
Subtask ID:
Objetivo:
Escopo permitido:
Arquivos permitidos:
Arquivos proibidos:
Entrada obrigatoria:
Saida esperada:
Criterio de aceite:
Limites:
```

Subtarefa sem contrato claro MUST NOT ser delegada.

---

## Responsabilidade do orquestrador

O orquestrador MUST:

- decidir se delega ou executa diretamente;
- definir subtarefas pequenas;
- evitar sobreposicao de arquivos entre subagentes;
- informar que subagentes nao devem reverter mudancas de outros;
- revisar achados recebidos;
- integrar somente o que preserva a filosofia do repo;
- resolver conflitos;
- executar ou solicitar validacao final;
- emitir o veredito final.

O orquestrador MUST NOT:

- delegar decisao de arquitetura final;
- delegar aprovacao de governanca;
- aceitar output de subagente sem revisao;
- esconder incerteza;
- marcar PASS sem evidencia.

---

## Responsabilidade dos subagentes

Subagentes MAY:

- investigar uma pergunta delimitada;
- implementar uma fatia com arquivos definidos;
- revisar uma mudanca especifica;
- validar criterios objetivos;
- apontar riscos e inconsistencias.

Subagentes MUST NOT:

- ampliar escopo por conta propria;
- alterar arquivos fora do escopo permitido;
- decidir veredito final;
- alterar `MANIFEST.md`, `governance/`, registry, remediation ou evals sem autorizacao explicita do orquestrador;
- substituir fonte primaria por opiniao propria;
- resolver conflito normativo como decisor final.

---

## Saidas oficiais

Quando o sizing concluir que a tarefa e direta:

```txt
EXECUTE_DIRECT
Reason:
Context needed:
Validation:
```

Quando concluir que deve delegar:

```txt
DECOMPOSE_AND_DELEGATE
Reason:
Subtasks:
Shared context:
Orchestrator validation:
```

Quando a tarefa for grande, mas nao puder ser decomposta com seguranca:

```txt
BLOCKED_FOR_DECOMPOSITION
Reason:
Missing decision:
Risk:
Suggested clarification:
```

---

## Relacao com Small Model Execution Mode

Small models execute bounded tasks.

Delegation Governance decide quando uma tarefa deixa de ser bounded.

Modelo pequeno pode executar subtarefa delegada somente se:

- a subtarefa tiver contrato claro;
- o contexto for explicitamente selecionado;
- nao houver governanca, arquitetura, safety critica ou veredito final;
- a saida for verificavel pelo orquestrador.

---

## Posicao na governanca

Esta feature deve ser representada por artefatos existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra operacional de composicao e escalacao | `governance/composition/context-composition.md` |
| skill de decomposicao e orquestracao | `skills/orchestration/` |
| hook de sizing quando aplicavel | `prompts/hooks/` |
| regra de limites de delegacao | `rules/architecture/` ou `rules/quality/` |
| explicacao humana | `README.md` |
| eval de comportamento | `evals/manual-regression-suite.md` |
| resultado de validacao | `evals/` |

Nao criar diretorio novo para subagentes.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/delegation-governance-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Criar ou atualizar skill de `Task Decomposition & Orchestration`.
- Criar hook leve de `size-task-for-delegation` se houver ganho operacional.
- Adicionar regra de limites de delegacao.
- Atualizar `governance/composition/context-composition.md` com sizing e delegacao.
- Atualizar `README.md` e `INDEX.md` com explicacao curta.
- Adicionar eval manual com casos de tarefa pequena, tarefa grande, delegacao indevida e veredito final.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.
- Atualizar `governance/authoring/artifact-registry.md` se a feature virar artefato critico.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Definir criterios de sizing | Orquestrador | spec | Limite entre executar e delegar | Criterios objetivos e simples |
| 2 | Definir contrato de subtarefa | Governanca | spec, skill | Delegacao verificavel | Toda subtarefa tem entrada, saida e limite |
| 3 | Implementar skill | Orquestracao | `skills/orchestration/` | Decomposicao operacional | Orquestrador mantem veredito |
| 4 | Implementar hook opcional | PromptOps | `prompts/hooks/` | Sizing reutilizavel | Hook nao executa tarefa final |
| 5 | Atualizar composicao | Governanca | `governance/composition/context-composition.md` | Fluxo reconhece sizing e delegacao | Nao carrega contexto amplo por padrao |
| 6 | Atualizar roteadores | Docs | `README.md`, `INDEX.md` | Descoberta humana e LLM clara | Texto curto, sem duplicar policy |
| 7 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Regressao coberta | Inclui EXECUTE_DIRECT, DECOMPOSE_AND_DELEGATE e BLOCKED_FOR_DECOMPOSITION |
| 8 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Gates rastreados | PASS somente com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe criterio claro para decidir se tarefa e direta ou grande;
- tarefa grande pode virar subtarefas pequenas e verificaveis;
- subagentes recebem escopo, arquivos permitidos, saida e limite;
- subagentes nao decidem veredito final;
- orquestrador revisa e integra outputs;
- ha saidas oficiais `EXECUTE_DIRECT`, `DECOMPOSE_AND_DELEGATE` e `BLOCKED_FOR_DECOMPOSITION`;
- `Small Model Execution Mode` continua valido para subtarefas bounded;
- evals cobrem delegacao correta e delegacao indevida;
- documentacao humana explica quando usar e quando nao usar delegacao.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Delegar tarefa simples | Custo e atraso | Task sizing antes de delegar |
| Subagente ampliar escopo | Drift e conflito | Contrato de subtarefa com arquivos permitidos e proibidos |
| Orquestrador terceirizar veredito | Falha de governanca | Veredito final obrigatorio do orquestrador |
| Subagentes editarem mesmo arquivo | Conflito e retrabalho | Write sets disjuntos por subtarefa |
| Delegacao virar arquitetura pesada | Aumento de custo cognitivo | Sem novo diretorio e sem runtime obrigatorio |
| Aceitar output sem revisao | Baixa confiabilidade | Review e integrate antes do verdict |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Delegation Governance aprovado como camada de sizing, decomposicao e orquestracao
Restricao: subagentes executam partes; o orquestrador mantem responsabilidade por escopo, integracao e veredito final
```

---

## Limites

Esta spec define governanca de delegacao.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../skills/`, `../../prompts/`, `../../evals/`, `../../_memory/` ou controles externos de runtime.
