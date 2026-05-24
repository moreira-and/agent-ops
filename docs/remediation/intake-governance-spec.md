# Spec: Intake Governance

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir a introducao de uma camada de `Intake Governance` no `agent-ops` para validar pedidos humanos antes da descoberta e injecao de contexto.

O novo fluxo-alvo passa a ser:

```txt
intake -> find -> select -> inject -> execute
```

Esta spec nao cria uma taxonomia paralela. Ela orienta uma evolucao pequena e governada para reduzir dano causado por pedidos humanos vagos, incompletos, contraditorios, perigosos ou sem criterio de sucesso.

---

## Problema

O fluxo atual `find -> select -> inject` governa bem a composicao de contexto, mas assume que a entrada humana ja esta minimamente clara.

Em uso profissional, essa premissa e fraca. Pessoas com baixo conhecimento tecnico ou baixo senso operacional podem pedir:

- acao destrutiva sem perceber;
- mudanca ampla sem escopo;
- "melhore", "arrume" ou "otimize" sem criterio;
- decisao sobre dados sensiveis sem autorizacao;
- execucao tecnica sem informar ambiente, permissao ou restricoes;
- resultado regulatorio, juridico ou financeiro sem contexto suficiente;
- trabalho impossivel ou contraditorio.

Sem uma camada anterior, o agente pode iniciar `find` a partir de uma intencao ruim e selecionar contexto inadequado.

---

## Objetivo

Adicionar uma etapa barata de triagem antes de `find`.

A etapa `intake` MUST decidir uma das quatro saidas:

| Saida | Quando usar |
|---|---|
| `READY_TO_FIND` | Pedido claro, seguro o suficiente e com criterio minimo de sucesso |
| `NEEDS_CLARIFICATION` | Falta informacao necessaria para executar sem improviso |
| `NEEDS_APPROVAL` | Ha risco alto, acao destrutiva, impacto amplo ou dependencia de autorizacao |
| `REFUSE_OR_REDIRECT` | Pedido proibido, inseguro, fora de escopo ou impossivel de cumprir com seguranca |

---

## Nao objetivos

Nao fazer nesta feature:

- criar um novo diretorio raiz `intake/`;
- transformar todo pedido simples em formulario;
- bloquear tarefas seguras por excesso de processo;
- carregar `docs/` ou `evals/` por padrao;
- criar automacao externa, runtime, UI ou ferramenta;
- substituir `prompts/`, `rules/`, `skills/` ou `governance/`;
- criar uma politica corporativa extensa;
- reescrever todos os prompts existentes.

---

## Posicao na governanca

`Intake Governance` e uma camada operacional anterior a descoberta de contexto.

Ela nao altera a taxonomia raiz v0.1. Ela deve ser representada com artefatos ja existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra de qualidade da entrada humana | `rules/quality/user-input-quality.md` |
| checkpoint operacional | `prompts/hooks/validate-user-intent.md` |
| capacidade reutilizavel de triagem | `skills/orchestration/intake-governance.md` |
| roteamento humano/LLM | `README.md`, `INDEX.md`, READMEs locais |
| validacao de comportamento | `evals/manual-regression-suite.md` |

Motivo: o repositorio ja possui categorias suficientes. Criar um diretorio raiz novo aumentaria custo cognitivo antes de provar necessidade.

---

## Modelo operacional

O modelo oficial deve evoluir de:

```txt
find -> select -> inject
```

para:

```txt
intake -> find -> select -> inject -> execute
```

### intake

Validar a entrada humana antes da busca por contexto.

O intake deve classificar:

- intencao;
- escopo;
- ambiguidade;
- risco;
- permissao necessaria;
- dados sensiveis;
- criterio minimo de sucesso;
- proxima acao permitida.

### find

Descobrir os artefatos candidatos somente depois que a intencao estiver suficientemente entendida.

### select

Escolher o menor conjunto de artefatos necessario.

### inject

Carregar somente o contexto selecionado.

### execute

Executar dentro dos limites definidos pelo intake e pelos artefatos injetados.

---

## Contrato do hook `validate-user-intent`

O hook `prompts/hooks/validate-user-intent.md` MUST:

- receber o pedido original do usuario;
- identificar objetivo declarado e objetivo inferido;
- listar lacunas criticas;
- classificar risco;
- decidir uma das quatro saidas do intake;
- formular perguntas objetivas quando precisar de esclarecimento;
- exigir aprovacao explicita para acao destrutiva, irreversivel ou de alto impacto;
- recusar ou redirecionar pedido inseguro;
- nao executar a tarefa final;
- nao carregar contexto especializado por habito.

O hook MUST NOT:

- substituir o prompt executor;
- virar checklist enciclopedico;
- pedir esclarecimento para tarefas triviais;
- inventar requisito ausente;
- assumir permissao para acao destrutiva;
- tratar documentacao humana como fonte normativa.

---

## Contrato da rule `user-input-quality`

A rule `rules/quality/user-input-quality.md` MUST definir criterios objetivos para avaliar uma entrada humana.

Ela deve cobrir, no minimo:

- pedido vago;
- pedido contraditorio;
- falta de escopo;
- falta de criterio de aceite;
- acao destrutiva;
- dados sensiveis;
- alto impacto operacional;
- decisao regulatoria, juridica ou financeira;
- solicitacao fora do escopo do repositorio;
- quando seguir sem perguntar para nao travar o fluxo.

A rule MUST diferenciar:

- ambiguidade toleravel;
- ambiguidade bloqueante;
- risco baixo;
- risco alto;
- pergunta necessaria;
- aprovacao necessaria;
- recusa ou redirecionamento.

---

## Contrato da skill `intake-governance`

A skill `skills/orchestration/intake-governance.md` SHOULD conter o procedimento reutilizavel de triagem.

Ela deve explicar como:

- decompor o pedido em intencao, escopo, risco e criterio de sucesso;
- evitar perguntas desnecessarias;
- manter o intake barato;
- produzir uma decisao curta;
- encaminhar para `find -> select -> inject`;
- preservar limites de seguranca sem travar trabalho seguro.

A skill SHOULD referenciar:

- `../../rules/quality/user-input-quality.md`
- `../../prompts/hooks/validate-user-intent.md`
- `../../governance/composition/context-composition.md`

---

## Mudancas esperadas

### Obrigatorias

- Criar `rules/quality/user-input-quality.md`.
- Criar `prompts/hooks/validate-user-intent.md`.
- Criar `skills/orchestration/intake-governance.md`.
- Atualizar `MANIFEST.md` para declarar o fluxo `intake -> find -> select -> inject -> execute`.
- Atualizar `governance/composition/context-composition.md` para posicionar `intake` antes de `find`.
- Atualizar `README.md` para explicar a camada de intake de forma curta.
- Atualizar `INDEX.md` para apontar o hook de intake quando o pedido humano estiver ambiguidade ou risco.
- Atualizar READMEs locais afetados:
  - `rules/quality/README.md`
  - `prompts/hooks/README.md`
  - `skills/orchestration/README.md`
- Adicionar eval minimo em `evals/manual-regression-suite.md`.
- Registrar resultado manual em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.

### Condicionais

- Atualizar prompts existentes somente se eles declararem diretamente o fluxo antigo como completo.
- Atualizar `docs/templates/new-artifact.md` se o template atual impedir declarar etapa de intake.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Inventariar referencias ao fluxo antigo | Orquestrador | `MANIFEST.md`, `README.md`, `governance/`, `prompts/`, `docs/` | Lista curta de pontos normativos | Nenhuma alteracao cega em massa |
| 2 | Definir rule de qualidade de entrada | Governanca de qualidade | `rules/quality/user-input-quality.md`, `rules/quality/README.md` | Criterios objetivos de entrada ruim | Distingue perguntar, aprovar, executar e recusar |
| 3 | Criar hook operacional | Prompt engineer | `prompts/hooks/validate-user-intent.md`, `prompts/hooks/README.md` | Checkpoint de intake criado | Produz `READY_TO_FIND`, `NEEDS_CLARIFICATION`, `NEEDS_APPROVAL` ou `REFUSE_OR_REDIRECT` |
| 4 | Criar skill reutilizavel | Especialista de orquestracao | `skills/orchestration/intake-governance.md`, `skills/orchestration/README.md` | Procedimento de triagem reutilizavel | Mantem intake barato e referencia rule/hook por caminho |
| 5 | Atualizar governanca central | Maintainer | `MANIFEST.md`, `governance/composition/context-composition.md` | Fluxo oficial evolui sem quebrar seletividade | Fica claro que intake antecede find e nao injeta repositorio |
| 6 | Atualizar roteadores | Documentacao | `README.md`, `INDEX.md` | Humanos e LLMs sabem quando usar intake | Explicacao curta, sem duplicar rule/hook |
| 7 | Adicionar evals | QA de IA | `evals/manual-regression-suite.md`, novo resultado em `evals/` | Casos cobrem entrada ruim | Inclui vagueza, risco destrutivo e pedido seguro que nao deve travar |
| 8 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Feature rastreavel | Gates PASS/FAIL com evidencia |
| 9 | Validar | Orquestrador | repo | Checks finais | `git diff --check`; nenhum README sem status; nenhum caminho inventado |

---

## Criterios de aceite

A feature esta pronta quando:

- O fluxo oficial aparece como `intake -> find -> select -> inject -> execute`.
- `intake` e definido como triagem barata de entrada humana, nao como novo carregamento de contexto.
- `rules/quality/user-input-quality.md` existe e diferencia ambiguidade, risco, aprovacao e recusa.
- `prompts/hooks/validate-user-intent.md` existe e produz uma das quatro saidas oficiais.
- `skills/orchestration/intake-governance.md` existe e referencia rule/hook/governance por caminho.
- `README.md` e `INDEX.md` indicam quando usar intake sem virar documentacao extensa.
- `governance/composition/context-composition.md` declara que `intake` acontece antes de `find`.
- `evals/` contem pelo menos tres casos:
  - pedido vago que exige esclarecimento;
  - pedido destrutivo que exige aprovacao;
  - pedido simples que deve seguir para `find` sem friccao indevida.
- Nenhum artefato novo duplica norma primaria de outro arquivo.
- Nenhum diretorio versionado fica sem `README.md`.
- `git diff --check` passa.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Intake virar burocracia | Agente pergunta demais e trava tarefas seguras | Rule deve definir ambiguidade toleravel e baixo risco |
| Intake virar prompt executor | Mistura triagem com execucao | Hook deve terminar em decisao, pergunta, aprovacao ou recusa |
| Criar taxonomia paralela | Aumenta carga cognitiva | Usar `rules/`, `prompts/hooks/` e `skills/` existentes |
| Regras duplicadas em hook e skill | Drift semantico | Rule e fonte primaria; hook e skill referenciam por caminho |
| Agente usar intake para carregar mais contexto | Aumenta custo | Intake deve operar antes de `find` com contrato minimo |
| Falta de friccao para alto risco | Acoes perigosas passam | `NEEDS_APPROVAL` obrigatorio para destrutivo, irreversivel ou amplo impacto |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Intake Governance aprovado como camada barata anterior a find
Fluxo oficial: intake -> find -> select -> inject -> execute
Restricao: intake nao e diretorio raiz, nao e contexto padrao e nao substitui guardrails de runtime
```

---

## Limites

Esta spec orienta a implementacao de `Intake Governance`.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../prompts/`, `../../skills/` ou `../../evals/`.
