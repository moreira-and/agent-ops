# Spec: Hygiene Governance

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir uma feature para manter o repositorio limpo por meio de verificacoes mecanicas, baratas e objetivas.

Regra central:

```txt
Garbage mecanico deve ser bloqueado cedo; julgamento semantico deve escalar para auditoria ou lifecycle.
```

---

## Problema

Repositorios de contexto operacional crescem rapido.

Sem higiene mecanica, o `agent-ops` pode acumular:

- arquivos vazios;
- arquivos temporarios;
- lixo de editor;
- caminhos quebrados;
- READMEs desatualizados;
- specs nao registradas;
- resultados de eval nao registrados;
- artefatos novos sem tipo ou finalidade;
- diretorios vazios sem justificativa;
- referencias a arquivos removidos;
- arquivos fora do diretorio esperado de forma obvia.

Esse garbage aumenta custo humano, custo de contexto e risco de drift.

---

## Objetivo

Criar `Hygiene Governance` para:

- detectar garbage mecanico cedo;
- bloquear inconsistencias objetivas antes de commit;
- manter roteadores e READMEs sincronizados;
- impedir arquivos orfaos simples;
- reduzir ruido antes que vire Context Debt;
- preparar um futuro pre-commit barato;
- preservar simplicidade e baixo custo.

---

## Nao objetivos

Nao fazer nesta feature:

- apagar legado automaticamente;
- decidir valor semantico de artefatos;
- substituir Context Debt Audit;
- substituir Artifact Lifecycle;
- substituir Artifact Synchronization;
- criar automacao obrigatoria neste momento;
- rodar auditoria profunda em toda mudanca;
- bloquear mudanca pequena por formalismo excessivo;
- criar dependencia de ferramenta externa.

---

## Definicao

`Hygiene Governance` e o dominio que regula limpeza mecanica do repositorio.

A feature operacional e:

```txt
Repository Hygiene Gate
```

Ela responde:

```txt
Existe garbage mecanico, referencia quebrada ou registro basico ausente?
```

---

## Escopo do gate

O gate MAY bloquear:

- arquivo vazio sem justificativa;
- diretorio vazio sem README ou spec;
- arquivo temporario de editor;
- arquivo binario inesperado;
- Markdown fora do padrao minimo;
- artefato novo sem `Tipo do artefato`;
- artefato novo sem `Finalidade`;
- spec em `docs/remediation/` sem registro no README local;
- resultado de eval sem registro em `evals/README.md`;
- hook novo sem registro em `prompts/hooks/README.md`;
- rule nova sem registro no README local;
- skill nova sem registro no README local;
- caminho quebrado em roteador ou registry;
- referencia a arquivo removido;
- lixo de conflito de merge.

---

## Fora do escopo do gate

O gate MUST NOT decidir sozinho:

- se um artefato agrega valor semantico;
- se uma skill deveria virar rule;
- se uma rule deveria virar governance;
- se um legado deve ser apagado;
- se uma feature esta pronta para producao;
- se um arquivo deve ser fundido, dividido ou depreciado por criterio conceitual.

Esses casos devem escalar para:

- `Context Debt Audit`;
- `Artifact Lifecycle`;
- `Artifact Synchronization`;
- revisao do orquestrador;
- decisao humana quando houver risco.

---

## Relacao com legado

Legado nao e garbage automaticamente.

Regra:

```txt
Legado nao e garbage ate existir evidencia, substituto, nota de migracao e aprovacao.
```

O Hygiene Gate MAY apontar candidato a legado problematico, mas MUST NOT remover.

Fluxo correto:

```txt
detectado candidato a legado
-> Context Debt Audit
-> DEPRECATE ou MERGE
-> Artifact Lifecycle
-> sync targets
-> remocao explicita em etapa posterior
```

---

## Saidas oficiais

Use uma das saidas:

```txt
PASS
Reason:
Evidence:
```

```txt
FAIL_GARBAGE
Reason:
File:
Required fix:
```

```txt
FAIL_BROKEN_REFERENCE
Reason:
Reference:
Required fix:
```

```txt
FAIL_MISSING_REGISTRATION
Reason:
Artifact:
Expected registry or README:
```

```txt
ESCALATE_CONTEXT_DEBT
Reason:
Artifact:
Why semantic review is needed:
```

```txt
ESCALATE_LIFECYCLE
Reason:
Artifact:
Lifecycle decision needed:
```

---

## Posicao na governanca

Esta feature deve ser representada por artefatos existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra de higiene do repositorio | `governance/quality/repository-hygiene-standard.md` |
| hook de validacao | `prompts/hooks/validate-repository-hygiene.md` |
| skill opcional de verificacao | `skills/review/` ou `skills/orchestration/` apenas se necessario |
| eval de regressao | `evals/manual-regression-suite.md` |
| resultado de validacao | `evals/` |

Skill dedicada nao e obrigatoria no primeiro momento.

Nao criar novo diretorio para hygiene.

---

## Relacao com features existentes

### Context Debt Audit

Hygiene Gate detecta garbage mecanico.

Context Debt Audit julga valor, redundancia, local correto e custo cognitivo.

### Artifact Synchronization

Hygiene Gate detecta registro basico ausente.

Artifact Synchronization decide sync targets por impacto.

### Artifact Lifecycle

Hygiene Gate detecta possivel legado ou arquivo orfao.

Artifact Lifecycle governa depreciacao, replacement, migration note e remocao.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/hygiene-governance-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Criar `governance/quality/repository-hygiene-standard.md`.
- Criar `prompts/hooks/validate-repository-hygiene.md`.
- Atualizar `governance/composition/context-composition.md` para reconhecer hygiene check sob demanda.
- Atualizar `README.md` e `INDEX.md` com explicacao curta.
- Adicionar eval manual com casos de garbage, referencia quebrada, registro ausente, legado e PASS limpo.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.
- Atualizar `governance/authoring/artifact-registry.md` se a feature virar artefato critico.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Definir escopo mecanico | Governanca | spec | Garbage objetivo delimitado | Nao decide valor semantico |
| 2 | Criar standard | Governanca de qualidade | `governance/quality/` | Criterio reutilizavel | Bloqueios objetivos |
| 3 | Criar hook | PromptOps | `prompts/hooks/` | Checkpoint sob demanda | Produz saidas oficiais |
| 4 | Atualizar composition | Governanca | `governance/composition/context-composition.md` | Check selecionavel | Nao entra por padrao |
| 5 | Atualizar roteadores | Docs | `README.md`, `INDEX.md` | Discovery claro | Texto curto e sem duplicar spec |
| 6 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Regressao coberta | Cobre garbage e escalacao |
| 7 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Gates rastreados | PASS somente com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe criterio claro para garbage mecanico;
- existe criterio claro para referencia quebrada;
- existe criterio claro para registro basico ausente;
- existe escalacao para Context Debt quando a decisao for semantica;
- existe escalacao para Lifecycle quando houver legado/depreciacao;
- a feature nao apaga arquivos automaticamente;
- a feature nao entra na composicao padrao;
- evals cobrem:
  - arquivo temporario;
  - artefato novo sem tipo/finalidade;
  - referencia quebrada;
  - spec sem registro;
  - legado que deve escalar, nao apagar;
  - repo limpo com PASS.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Gate virar burocracia | Custo alto | Apenas checks mecanicos e sob demanda |
| Apagar legado util | Perda de conhecimento | Hygiene nunca remove automaticamente |
| Confundir garbage com context debt | Decisao errada | Escalar julgamento semantico |
| Bloquear mudanca pequena | Friccao excessiva | Typos e mudancas locais simples passam se nao quebram referencia |
| Pre-commit pesado futuro | Baixa aderencia | Separar hygiene barato de auditoria profunda |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Hygiene Governance aprovado como gate barato para garbage mecanico, referencias quebradas e registro basico ausente
Restricao: nao apaga legado, nao decide valor semantico e nao vira auditoria pesada de pre-commit
```

---

## Limites

Esta spec define governanca de higiene mecanica do repositorio.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../evals/`, `Context Debt Audit`, `Artifact Lifecycle` ou controles externos de pre-commit.
