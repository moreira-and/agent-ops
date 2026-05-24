# Spec: Context Debt Audit

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir uma auditoria leve para detectar e conter divida de arquitetura informacional no `agent-ops`.

Regra central:

```txt
O repo deve crescer por valor operacional, nao por acumulo de artefatos.
```

---

## Problema

O `agent-ops` ganhou governance, intake, memory, registry, evals, remediation, small model mode e delegation governance.

Essas camadas aumentam controle, mas tambem aumentam risco de:

- redundancia semantica;
- artefatos longos demais;
- diretorios com responsabilidade pouco clara;
- docs explicativas virarem prompt operacional;
- rules absorverem governance;
- skills virarem normas;
- hooks virarem workflows;
- evals virarem documentacao;
- registry virar catalogo total;
- custo de contexto subir sem ganho real;
- manutencao humana ficar pesada.

Isso e **Information Architecture Debt**.

No contexto deste repo, o nome operacional da feature e `Context Debt Audit`.

---

## Objetivo

Criar `Context Debt Audit` para:

- auditar se um artefato agrega valor operacional real;
- detectar duplicidade, sobreposicao e excesso de texto;
- validar responsabilidade unica;
- validar se o arquivo esta no diretorio certo;
- medir custo cognitivo e custo de contexto;
- impedir crescimento por ansiedade de governanca;
- preservar simplicidade, baixo custo e alta legibilidade;
- orientar consolidacao, corte, divisao ou realocacao de artefatos.

---

## Nao objetivos

Nao fazer nesta feature:

- criar novo diretorio raiz;
- criar processo obrigatorio para toda edicao pequena;
- catalogar todos os arquivos;
- medir tokens com ferramenta externa obrigatoria;
- substituir `MANIFEST.md`;
- substituir `artifact-synchronization-policy.md`;
- bloquear evolucao util;
- transformar o repo em governanca corporativa pesada;
- apagar artefatos sem revisao humana.

---

## Definicao

`Context Debt Audit` e uma auditoria de arquitetura informacional aplicada a artefatos, diretorios ou mudancas.

Ela responde:

```txt
Este artefato ainda prova valor, responsabilidade unica, local correto e custo justificavel?
```

---

## Quando usar

Use Context Debt Audit quando:

- o repo parecer grande, redundante ou caro;
- houver criacao de nova feature governada;
- uma spec gerar varios artefatos novos;
- um diretorio ganhar muitos arquivos;
- houver duvida se um arquivo deve existir;
- houver sobreposicao entre prompts, skills, rules, governance e docs;
- uma mudanca alterar roteadores, composition, registry ou evals;
- antes de v0.1, release ou revisao de arquitetura.

---

## Quando nao usar

Nao use Context Debt Audit quando:

- a mudanca for typo local;
- a tarefa tiver escopo pequeno e criterio de aceite local;
- o custo da auditoria for maior que o risco;
- ja houver uma auditoria equivalente registrada para a mesma mudanca;
- a pergunta for apenas sobre conteudo tecnico de engenharia de dados.

---

## Eixos de auditoria

### 1. Valor operacional

O artefato MUST provar pelo menos um valor:

- melhora selecao de contexto;
- reduz ambiguidade;
- reduz risco operacional;
- evita duplicidade;
- melhora manutencao;
- melhora validacao;
- orienta execucao recorrente.

Se nao provar valor, SHOULD ser removido, fundido ou movido para docs.

### 2. Responsabilidade unica

O artefato SHOULD ter uma responsabilidade principal clara.

Sinais de violacao:

- mistura regra, procedimento, exemplo e politica;
- tenta ser README, prompt e eval ao mesmo tempo;
- tem multiplos publicos sem separacao;
- contem tutorial longo dentro de rule ou hook.

### 3. Local correto

O artefato MUST estar no diretorio que melhor representa sua funcao:

| Conteudo | Local esperado |
|---|---|
| norma estrutural | `governance/` |
| restricao de output ou entrada humana | `rules/` |
| capacidade operacional reutilizavel | `skills/` |
| ponto de entrada ou checkpoint | `prompts/` ou `prompts/hooks/` |
| explicacao humana | `docs/` |
| validacao de comportamento | `evals/` |
| memoria auxiliar | `_memory/` |

### 4. Redundancia

Conteudo repetido SHOULD apontar para uma fonte primaria.

Duplicidade aceitavel:

- resumo curto em README;
- roteamento por caminho;
- criterio repetido de forma compacta para orientar discovery.

Duplicidade nao aceitavel:

- mesma regra completa em varios arquivos;
- spec copiada para README;
- governance embutida em prompt;
- eval explicando norma em vez de validar comportamento.

### 5. Custo cognitivo

O artefato SHOULD ser curto o suficiente para ser usado sem leitura excessiva.

Sinais de custo alto:

- muitas secoes sem decisao operacional;
- listas longas sem criterio;
- exemplos extensos dentro do artefato operacional;
- linguagem abstrata sem acao;
- dependencias demais para uma tarefa comum.

### 6. Custo de contexto

O artefato MUST NOT ser carregado por padrao se for auxiliar, humano, validacao ou historico.

Artefatos extensos SHOULD ser:

- resumidos em roteadores;
- selecionados sob demanda;
- divididos somente quando houver responsabilidade autonoma;
- movidos para docs ou evals quando forem explicativos.

### 7. Governanca real

Uma regra declarada deve ter caminho de enforcement ou validacao.

Sinais de governanca falsa:

- policy sem criterio de aceite;
- guardrail sem hook, rule ou eval;
- README prometendo comportamento que composition nao reconhece;
- registry citando sync targets que ninguem consulta.

---

## Saidas oficiais

Use uma das saidas:

```txt
KEEP
Reason:
Evidence:
Cost:
Next review:
```

```txt
TRIM
Reason:
Sections to reduce:
Primary source to keep:
Expected reduction:
```

```txt
MERGE
Reason:
Source artifact:
Target artifact:
Conflict to resolve:
```

```txt
MOVE
Reason:
Current path:
Target path:
Sync targets:
```

```txt
SPLIT
Reason:
Current artifact:
New responsibilities:
New target paths:
```

```txt
DEPRECATE
Reason:
Replacement:
Migration note:
Removal condition:
```

---

## Severidade

| Severidade | Criterio |
|---|---|
| P0 | Bloqueia uso confiavel ou cria risco operacional |
| P1 | Compromete governanca, safety, precedencia ou manutencao critica |
| P2 | Aumenta custo, duplicidade ou confusao de forma relevante |
| P3 | Melhoria incremental de clareza ou economia |

---

## Posicao na governanca

Esta feature deve ser representada por artefatos existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra de economia e responsabilidade | `rules/quality/` ou `governance/quality/` |
| hook de auditoria quando aplicavel | `prompts/hooks/` |
| skill de revisao de arquitetura de contexto | `skills/review/` ou `skills/orchestration/` |
| criterio de sync | `governance/lifecycle/artifact-synchronization-policy.md` |
| eval de regressao | `evals/manual-regression-suite.md` |
| resultado de validacao | `evals/` |

Nao criar diretorio novo para `context debt`.

---

## Relacao com features existentes

### Artifact Synchronization

Artifact Synchronization pergunta:

```txt
Quais arquivos precisam ser revisados quando algo muda?
```

Context Debt Audit pergunta:

```txt
Este arquivo ainda deveria existir deste jeito?
```

### Delegation Governance

Delegation Governance ajuda a quebrar uma tarefa grande.

Context Debt Audit avalia se a propria estrutura resultante ficou cara, redundante ou mal separada.

### Small Model Execution Mode

Small Model Execution Mode reduz contexto para modelos pequenos.

Context Debt Audit reduz o tamanho e a redundancia do proprio repositorio para que modelos pequenos continuem uteis.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/context-debt-audit-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Criar regra ou standard de economia de contexto e responsabilidade.
- Criar hook leve de `validate-context-debt` se houver ganho operacional.
- Criar skill de `context-architecture-review`.
- Atualizar `governance/composition/context-composition.md` para reconhecer auditoria sob demanda.
- Atualizar `README.md` e `INDEX.md` com explicacao curta.
- Adicionar eval manual com casos de manter, cortar, fundir, mover e bloquear crescimento.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.
- Atualizar `governance/authoring/artifact-registry.md` se a feature virar artefato critico.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Definir eixos de auditoria | Governanca | spec | Criterios objetivos | Valor, responsabilidade, local, redundancia e custo definidos |
| 2 | Criar regra/standard | Governanca de qualidade | `governance/quality/` ou `rules/quality/` | Criterio reutilizavel | Nao duplica MANIFEST |
| 3 | Criar hook | PromptOps | `prompts/hooks/` | Checkpoint sob demanda | Hook nao executa reestruturacao |
| 4 | Criar skill | Review / Orquestracao | `skills/review/` ou `skills/orchestration/` | Auditoria operacional | Produz KEEP/TRIM/MERGE/MOVE/SPLIT/DEPRECATE |
| 5 | Atualizar composicao | Governanca | `governance/composition/context-composition.md` | Auditoria fica selecionavel | Nao entra por padrao |
| 6 | Atualizar roteadores | Docs | `README.md`, `INDEX.md` | Discovery claro | Texto curto e sem duplicar spec |
| 7 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Regressao coberta | Casos cobrem excesso, redundancia e local errado |
| 8 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Gates rastreados | PASS somente com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe criterio claro para avaliar valor operacional real;
- existe criterio para detectar responsabilidade misturada;
- existe criterio para detectar arquivo no diretorio errado;
- existe criterio para detectar redundancia aceitavel e inaceitavel;
- existe criterio para decidir KEEP, TRIM, MERGE, MOVE, SPLIT ou DEPRECATE;
- a auditoria nao entra na composicao padrao;
- roteadores explicam a feature sem duplicar a spec;
- evals cobrem pelo menos um caso de excesso e um caso de artefato necessario;
- nenhum novo diretorio raiz foi criado.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Auditoria virar burocracia | Custo alto | Uso sob demanda, nao padrao |
| Cortar artefato util | Perda de governanca | Exigir evidencia e fonte primaria |
| Fundir demais | Arquivos grandes e confusos | Responsabilidade unica como criterio |
| Fragmentar demais | Mais roteamento e custo | Novo arquivo so com autonomia semantica |
| Confundir docs com prompt | Contexto caro | Separar explicacao humana de instrucao operacional |
| Registry virar catalogo total | Manutencao pesada | Registry so para artefatos criticos |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Context Debt Audit aprovado como auditoria sob demanda para conter crescimento, redundancia e custo cognitivo
Restricao: nao vira fluxo obrigatorio para mudancas pequenas e nao cria novo diretorio raiz
```

---

## Limites

Esta spec define auditoria de arquitetura informacional.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../skills/`, `../../prompts/`, `../../evals/`, `../../_memory/` ou controles externos de runtime.
