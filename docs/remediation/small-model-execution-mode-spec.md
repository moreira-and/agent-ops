# Spec: Small Model Execution Mode

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir um modo operacional barato para modelos pequenos no `agent-ops`.

Regra central:

```txt
Small models execute bounded tasks; they do not govern, redesign, approve, or expand the system.
```

Em portugues:

```txt
Modelos pequenos executam tarefas delimitadas; nao governam, nao redesenham, nao aprovam e nao expandem o sistema.
```

---

## Problema

O `agent-ops` ganhou governanca real: intake, index, memory, registry, lifecycle, evals e remediation.

Isso melhora controle, mas cria risco de custo para modelos pequenos se eles tentarem carregar a governanca inteira antes de executar uma tarefa simples.

Modelo pequeno nao deve agir como arquiteto, auditor, maintainer de governanca ou decisor de seguranca critica.

Se fizer isso, o sistema fica:

- caro demais;
- lento demais;
- propenso a leitura indiscriminada;
- mais vulneravel a conflito normativo;
- ruim para tarefas simples;
- dependente de bom senso do modelo.

---

## Objetivo

Criar `Small Model Execution Mode` para:

- reduzir contexto inicial;
- limitar autonomia de modelos pequenos;
- preservar `intake -> find -> select -> inject -> execute`;
- permitir execucao barata de tarefas simples;
- exigir escalacao quando houver governanca, arquitetura, risco alto ou ambiguidade bloqueante;
- impedir que modelos pequenos atualizem taxonomia, manifesto, registry, policies ou grow sem revisao.

---

## Nao objetivos

Nao fazer nesta feature:

- criar runtime de roteamento de modelos;
- amarrar o repo a fornecedor ou modelo especifico;
- criar benchmark de modelos;
- substituir intake;
- remover governanca existente;
- permitir que modelo pequeno decida governanca;
- criar automacao obrigatoria;
- carregar registry, remediation, evals ou `_memory/` por padrao.

---

## Definicao

`Small Model Execution Mode` e um modo de operacao em que o agente:

- recebe uma tarefa delimitada;
- recebe contexto explicitamente selecionado;
- executa dentro do escopo;
- valida formato local quando aplicavel;
- pergunta ou escala quando faltar contexto critico;
- nao decide governanca.

---

## O que modelo pequeno pode fazer

Modelo pequeno MAY:

- seguir um prompt ja escolhido;
- aplicar uma rule especifica;
- usar uma skill especifica;
- preencher template;
- revisar formato simples;
- executar transformacao local e reversivel;
- responder com base em poucos artefatos;
- sinalizar lacuna;
- retornar `BLOCKED_OR_ESCALATE` quando a tarefa exceder escopo.

---

## O que modelo pequeno nao pode fazer

Modelo pequeno MUST NOT:

- alterar `MANIFEST.md`;
- alterar `governance/`;
- criar ou aprovar nova rule, skill, agent, prompt ou hook;
- decidir taxonomia;
- aprovar grow;
- resolver conflito normativo complexo;
- interpretar multiplas fontes concorrentes como decisor final;
- carregar `_memory/`, registry, remediation ou evals por conta propria;
- fazer auditoria ampla;
- decidir se uma operacao de alto risco e segura;
- executar acao destrutiva, irreversivel ou de amplo impacto sem escalacao;
- alterar `_distillation/` futura ou dados de treino.

---

## Condicoes para usar

Use Small Model Execution Mode quando a tarefa for:

- clara;
- pequena;
- baixo risco;
- delimitada;
- reversivel ou sem efeito externo;
- baseada em ate poucos artefatos explicitamente selecionados.

Nao use quando houver:

- ambiguidade bloqueante;
- conflito normativo;
- mudanca estrutural;
- seguranca operacional;
- dados sensiveis;
- aprovacao;
- grow;
- auditoria;
- design de taxonomia;
- alteracao de `MANIFEST.md`, `governance/`, registry, remediation ou evals.

---

## Contexto maximo recomendado

Para modelos pequenos, a composicao inicial SHOULD ter:

- no maximo 1 prompt;
- no maximo 1 rule principal;
- no maximo 1 skill principal;
- input da tarefa;
- formato de saida esperado.

Pode adicionar mais contexto somente se:

- houver motivo explicito;
- a tarefa continuar bounded;
- nao envolver governanca ou risco alto.

---

## Fluxo operacional

```txt
intake
-> se bounded e low risk: small model execute
-> se ambiguo, high impact ou governance: escalate
-> find
-> select minimal context
-> inject
-> execute
```

Regra pratica:

```txt
small model = executor
large model = governor / architect / auditor
```

---

## Saida de escalacao

Quando nao puder executar com seguranca, o modelo pequeno MUST retornar:

```txt
BLOCKED_OR_ESCALATE
Reason:
Missing context:
Risk:
Suggested next artifact:
Suggested escalation:
```

`Suggested next artifact` deve apontar no maximo um caminho inicial.

---

## Posicao na governanca

Esta feature deve ser representada por artefatos existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra operacional do modo | `governance/composition/context-composition.md` |
| roteamento barato | `INDEX.md` |
| explicacao humana | `README.md` |
| eval de comportamento | `evals/manual-regression-suite.md` |
| resultado de validacao | `evals/` |

Nao criar diretorio novo para modelos pequenos.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/small-model-execution-mode-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Atualizar `INDEX.md` com regra curta para modelos pequenos.
- Atualizar `governance/composition/context-composition.md` com `Small Model Execution Mode`.
- Atualizar `README.md` com explicacao curta.
- Adicionar eval manual em `evals/manual-regression-suite.md`.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.
- Atualizar `governance/authoring/artifact-registry.md` se a policy virar artefato critico.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Definir limites do modo | Orquestrador | spec | Escopo claro | Modelos pequenos nao governam |
| 2 | Atualizar composicao | Governanca | `governance/composition/context-composition.md` | Modo fica operacional | Limite de contexto e escalacao definidos |
| 3 | Atualizar roteadores | Docs | `INDEX.md`, `README.md` | Descoberta barata | Texto curto, sem duplicar policy |
| 4 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Casos cobrem executar e escalar | Inclui tarefa simples e tarefa de governanca |
| 5 | Registrar resultado | QA de IA | `evals/` | PASS/FAIL rastreavel | Resultado manual claro |
| 6 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Gates rastreados | ORQ com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe regra clara: modelos pequenos executam, nao governam;
- `INDEX.md` orienta modelos pequenos a comecar pelo menor roteador possivel;
- `context-composition.md` limita contexto inicial para modelos pequenos;
- modelo pequeno deve escalar governanca, arquitetura, seguranca, taxonomia, grow e auditoria;
- existe formato `BLOCKED_OR_ESCALATE`;
- registry, remediation, evals e `_memory/` nao entram por padrao;
- existe eval com:
  - tarefa simples que modelo pequeno pode executar;
  - tarefa de governanca que deve escalar;
  - tarefa ambigua que deve pedir intake ou escalacao;
  - tentativa de carregar repo inteiro que deve ser recusada.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Modelo pequeno carregar governanca demais | Custo alto e baixa qualidade | Limite de contexto e escalacao obrigatoria |
| Modelo pequeno decidir governanca | Drift estrutural | Proibir alteracao de manifesto, governance, registry e grow |
| Escalar demais | Perda de eficiencia | Permitir execucao de tarefas bounded e low-risk |
| Esconder lacuna | Saida errada | `BLOCKED_OR_ESCALATE` obrigatorio |
| Criar modo paralelo complexo | Mais carga cognitiva | Sem novo diretorio; atualizar apenas roteadores e composition |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Small Model Execution Mode aprovado como modo barato de execucao delimitada
Restricao: modelos pequenos nao governam, nao aprovam, nao redesenham e nao expandem o sistema
```

---

## Limites

Esta spec define limites operacionais para modelos pequenos.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../skills/`, `../../prompts/`, `../../evals/`, `../../_memory/` ou controles externos de runtime.
