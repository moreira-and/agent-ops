# Spec: Artifact Synchronization

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir uma governanca barata para manter artefatos sincronizados sem adicionar metadados pesados em todos os arquivos.

Esta feature combina:

- metadata minimo inline;
- registry central de artefatos;
- politica de sincronizacao por impacto.

Objetivo: facilitar atualizacao de docs, roteadores, memories, extensions futuras e distillation futura sem criar burocracia nem aumentar custo de contexto por padrao.

---

## Problema

O `agent-ops` esta crescendo com artefatos centrais, auxiliares e futuros diretorios como `_memory/`, `_extensions/` e `_distillation/`.

Sem uma regra de sincronizacao, cada mudanca pode exigir revisao manual ampla e cara:

- README raiz pode ficar desatualizado;
- `INDEX.md` pode apontar para rotas incompletas;
- `MANIFEST.md` pode nao refletir a estrutura real;
- `governance/composition/context-composition.md` pode perder regras de selecao;
- evals podem nao cobrir novas responsabilidades;
- memories podem apontar para fontes antigas;
- specs podem ficar desconectadas da implementacao.

O risco oposto tambem existe: colocar metadata completo em todo arquivo aumenta token cost e manutencao.

---

## Objetivo

Criar uma estrategia de sincronizacao que:

- reduza custo de manutencao;
- facilite busca na IDE;
- preserve fonte primaria unica;
- evite atualizar o repositorio inteiro por reflexo;
- deixe claro quais arquivos devem ser revisados quando outro muda;
- mantenha metadata inline minimo;
- centralize rastreabilidade em um registry leve.

---

## Nao objetivos

Nao fazer nesta feature:

- colocar bloco completo de metadata em todos os arquivos;
- exigir commit hash em todo artefato;
- criar automacao obrigatoria;
- criar banco externo;
- criar plugin, runtime ou ferramenta;
- transformar registry em fonte normativa primaria;
- substituir `MANIFEST.md`, `governance/`, `rules/`, `skills/`, `prompts/`, `docs/`, `evals/` ou `_memory/`.

---

## Nome recomendado

Conceito:

```txt
Artifact Synchronization
```

Artefatos recomendados:

- `governance/authoring/artifact-registry.md`
- `governance/lifecycle/artifact-synchronization-policy.md`

Termos relacionados:

- `Artifact Metadata Minimal Standard`
- `Artifact Registry`
- `Sync targets`
- `Impact class`

---

## Modelo proposto

### 1. Metadata minimo inline

Somente artefatos centrais ou criticos SHOULD receber no topo:

```txt
Artifact ID:
Kind:
```

Campos adicionais sao opcionais e devem ser raros:

```txt
Primary source:
Status:
Last reviewed:
Review cadence:
Reviewed against commit:
```

`Reviewed against commit` MAY ser usado apenas em auditoria, release ou artefato critico.

### 2. Registry central

O registry central concentra rastreabilidade:

```txt
governance/authoring/artifact-registry.md
```

Campos minimos:

```md
| Artifact ID | Path | Kind | Primary source | Status | Review cadence | Last reviewed | Sync targets |
|---|---|---|---|---|---|---|---|
```

O campo mais importante e `Sync targets`.

Ele responde:

```txt
Se este arquivo mudar, quais arquivos talvez precisem ser revisados?
```

### 3. Politica de sincronizacao por impacto

A politica define classes de impacto:

| Classe | Quando usar | Acao minima |
|---|---|---|
| `NONE` | Mudanca local sem efeito em roteamento, contrato ou comportamento | Nenhum sync externo |
| `LOCAL` | Muda escopo ou arquivo dentro de um diretorio | Revisar README local |
| `ROUTER` | Muda descoberta, nomes, estrutura ou pontos de entrada | Revisar `README.md`, `INDEX.md` e README local |
| `CONTRACT` | Muda comportamento, regra, guardrail, composicao ou precedencia | Revisar `MANIFEST.md`, `governance/`, hooks e evals aplicaveis |
| `AUXILIARY` | Muda `_memory/`, futura `_extensions/` ou futura `_distillation/` | Revisar registry, composition, root routers e evals aplicaveis |
| `RELEASE` | Muda readiness, resultado de auditoria ou criterio de versao | Revisar evals, remediation e registros de release |

---

## Posicao na governanca

`Artifact Synchronization` pertence a:

- `governance/authoring/` para registry e metadata minimo;
- `governance/lifecycle/` para politica de sincronizacao e revisao.

Nao criar `governance/registry/` neste momento.

Motivo: registry e suporte de autoria/manutencao, nao nova categoria operacional.

---

## Contrato de metadata inline

Metadata inline MUST ser pequeno.

Formato recomendado:

```txt
Artifact ID: <namespace.name>
Kind: <kind>
```

Exemplos:

```txt
Artifact ID: memory.lessons-learned
Kind: governed-memory
```

```txt
Artifact ID: governance.context-composition
Kind: governance
```

Regras:

- `Artifact ID` MUST ser estavel.
- `Kind` MUST usar termos ja reconhecidos pelo repo.
- Metadata inline MUST NOT duplicar registry completo.
- Artefatos simples MAY nao ter metadata inline.
- Artefatos criticos SHOULD ter metadata inline.

---

## Contrato do registry

`artifact-registry.md` SHOULD:

- listar apenas artefatos centrais, criticos ou auxiliares governados;
- mapear `Artifact ID` para `Path`;
- declarar `Kind`;
- declarar `Primary source`;
- declarar `Status`;
- declarar `Review cadence`;
- declarar `Last reviewed`;
- declarar `Sync targets`;
- nao substituir README local;
- nao substituir manifest;
- nao listar todos os arquivos do repositorio por obrigacao.

O registry e indice de sincronizacao, nao catalogo enciclopedico.

---

## Contrato da policy

`artifact-synchronization-policy.md` MUST:

- definir classes de impacto;
- orientar como escolher sync targets;
- definir quando atualizar README local, root README, INDEX, MANIFEST, governance, evals e remediation;
- impedir atualizacao em massa sem motivo;
- exigir registro minimo quando uma mudanca altera contrato ou comportamento;
- orientar como lidar com `_memory/`, `_extensions/` e `_distillation/`.

---

## Regras para diretorios auxiliares

Diretorios prefixados com `_` sao auxiliares.

### `_memory/`

Tipo: governed memory.

Sync targets provaveis:

- `README.md`
- `INDEX.md`
- `MANIFEST.md`
- `governance/composition/context-composition.md`
- `evals/manual-regression-suite.md`

### `_extensions/`

Tipo futuro: plugable context extension.

Sync targets provaveis:

- `README.md`
- `INDEX.md`
- `MANIFEST.md`
- `governance/composition/context-composition.md`
- `evals/`

### `_distillation/`

Tipo futuro: curated distillation data.

Sync targets provaveis:

- `README.md`
- `INDEX.md`
- `MANIFEST.md`
- `evals/README.md`
- policy especifica de dados, privacidade e schema

`_distillation/` MUST NOT armazenar chain-of-thought bruto, segredo, dado pessoal ou dado de cliente sem politica explicita.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/artifact-synchronization-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Criar `governance/authoring/artifact-registry.md`.
- Criar `governance/lifecycle/artifact-synchronization-policy.md`.
- Atualizar `governance/authoring/README.md`.
- Atualizar `governance/lifecycle/README.md`.
- Atualizar `MANIFEST.md` apenas se a politica virar parte oficial do contrato de v0.1.
- Adicionar eval manual para sincronizacao.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Inventariar artefatos criticos | Orquestrador | `MANIFEST.md`, `README.md`, `INDEX.md`, `governance/`, `_memory/`, `evals/` | Lista curta, nao catalogo total | Apenas artefatos com impacto real entram |
| 2 | Criar registry minimo | Governanca de autoria | `governance/authoring/artifact-registry.md` | Tabela com Artifact ID, path e sync targets | Registry cabe em leitura rapida |
| 3 | Criar policy de sync | Governanca de lifecycle | `governance/lifecycle/artifact-synchronization-policy.md` | Classes de impacto e acoes minimas | Mudanca sabe o que revisar sem varrer tudo |
| 4 | Aplicar metadata inline minimo | Maintainer | artefatos criticos selecionados | `Artifact ID` e `Kind` em poucos arquivos | Nenhum bloco pesado em folhas simples |
| 5 | Atualizar READMEs locais | Docs | `governance/authoring/README.md`, `governance/lifecycle/README.md` | Descoberta humana mantida | README prova existencia dos novos arquivos |
| 6 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Caso cobre sync targets | Eval evita drift em README/INDEX/MANIFEST |
| 7 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Feature rastreavel | Gates PASS/FAIL com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe registry central leve;
- existe policy de sincronizacao por impacto;
- metadata inline fica limitado a `Artifact ID` e `Kind` por padrao;
- artefatos simples nao recebem metadata desnecessario;
- registry define sync targets para artefatos criticos;
- `_memory/`, futura `_extensions/` e futura `_distillation/` tem regra de sincronizacao;
- `README.md`, `INDEX.md`, `MANIFEST.md`, `governance/composition/context-composition.md`, `evals/` e remediation aparecem como sync targets quando aplicavel;
- existe eval cobrindo mudanca que exige sync;
- `git diff --check` passa;
- nenhum diretorio versionado fica sem README.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Metadata inline virar tax | Mais tokens em todo arquivo | Limitar a `Artifact ID` e `Kind` em artefatos criticos |
| Registry virar catalogo total | Alto custo e manutencao | Listar apenas artefatos criticos ou auxiliares governados |
| Sync targets desatualizados | Falsa seguranca | Eval e review cadence |
| Commit hash manual envelhecer | Rastreabilidade falsa | `Reviewed against commit` opcional e raro |
| Policy virar burocracia | Atualizacoes lentas | Classes de impacto com acao minima |
| `_distillation/` vazar dado sensivel | Risco operacional e legal | Policy especifica antes de criar dados reais |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Artifact Synchronization aprovado como governanca leve de sincronizacao
Restricao: registry nao e fonte normativa primaria e metadata inline nao deve virar bloco pesado
```

---

## Limites

Esta spec orienta a implementacao de sincronizacao de artefatos.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../skills/`, `../../prompts/`, `../../docs/`, `../../evals/` ou `../../_memory/`.
