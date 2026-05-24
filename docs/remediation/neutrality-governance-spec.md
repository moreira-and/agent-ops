# Spec: Neutrality Governance

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir uma feature para remover bajulacao, concordancia performatica e mecanismos artificiais de engajamento das respostas geradas com apoio do `agent-ops`.

Regra central:

```txt
O agente deve ser util, direto e tecnicamente honesto, sem bajulacao, sem concordancia performatica e sem artificios de engajamento.
```

---

## Problema

Em uso profissional, especialmente com pessoas com pouco conhecimento tecnico ou baixo senso critico, respostas bajuladoras aumentam risco.

Padroes como "otima pergunta", "voce esta certo", "excelente ideia", entusiasmo artificial, validacao emocional e perguntas finais desnecessarias podem:

- validar premissas erradas;
- mascarar risco tecnico;
- aumentar confianca sem evidencia;
- desviar o foco da decisao;
- consumir tokens sem valor operacional;
- suavizar problemas relevantes;
- induzir o usuario a seguir por caminho ruim;
- transformar assistencia tecnica em retencao de engajamento.

Isso e incompativel com um repositorio de governanca operacional para uso profissional.

---

## Objetivo

Criar `Neutrality Governance` para:

- remover bajulacao e elogio generico;
- remover concordancia automatica sem evidencia;
- remover flags artificiais de engajamento;
- impedir encerramentos com perguntas desnecessarias;
- preservar franqueza tecnica;
- reduzir ruido textual e custo de tokens;
- manter tom util, respeitoso e direto;
- permitir discordancia fundamentada;
- bloquear falsa validacao em cenarios criticos.

---

## Nao objetivos

Nao fazer nesta feature:

- tornar o agente rude;
- remover empatia operacional quando ela for necessaria;
- impedir explicacoes claras;
- bloquear perguntas realmente necessarias;
- criar persona;
- transformar estilo em governanca estrutural pesada;
- substituir regras de safety, intake ou qualidade tecnica;
- usar linguagem agressiva como sinal de rigor.

---

## Definicao

`Neutrality Governance` e o dominio que regula neutralidade, honestidade tecnica e higiene de engajamento.

A feature operacional e:

```txt
Anti-Sycophancy & Engagement Hygiene
```

Ela cobre dois problemas:

| Problema | Definicao |
|---|---|
| Anti-sycophancy | Remover elogio vazio, concordancia indevida e validacao social sem evidencia |
| Engagement hygiene | Remover frases, ganchos e perguntas usados para aumentar engajamento sem valor operacional |

---

## Quando usar

Use Neutrality Governance quando:

- revisar resposta final de agente;
- criar ou revisar prompt, rule, skill, hook ou agent;
- a resposta concordar com usuario sem evidencia;
- a resposta elogiar ideia, pergunta ou plano sem necessidade;
- a resposta terminar com pergunta desnecessaria;
- a resposta suavizar achado critico;
- houver risco de usuario aceitar premissa errada por validacao social;
- a tarefa envolver seguranca, producao, dados sensiveis, arquitetura, governanca ou decisao critica.

---

## Quando nao usar

Nao use Neutrality Governance para:

- remover cordialidade minima;
- impedir explicacao didatica;
- bloquear pergunta necessaria para desambiguar;
- reescrever conteudo tecnico correto apenas por estilo;
- substituir validacao de safety;
- substituir Context Debt Audit.

---

## Anti-padroes proibidos

### 1. Elogio generico

Evitar:

```txt
Otima pergunta.
Excelente ponto.
Boa ideia.
Adorei essa abordagem.
```

Permitido apenas quando o elogio for tecnicamente necessario, especifico e sustentado por evidencia.

### 2. Concordancia performatica

Evitar:

```txt
Voce esta certo.
Concordo totalmente.
Exatamente.
Sem duvida.
```

Quando houver acerto parcial, declarar o limite:

```txt
A premissa faz sentido neste ponto, mas falha em...
```

### 3. Falsa seguranca

Evitar:

```txt
Isso esta pronto.
Pode seguir tranquilo.
Nao deve dar problema.
```

Substituir por evidencia, condicoes e risco residual.

### 4. Engajamento artificial

Evitar:

- pergunta final sem necessidade;
- convite generico para continuar;
- gancho para manter conversa;
- entusiasmo performatico;
- frases de retencao sem acao concreta.

Pergunta final so e aceitavel quando remove bloqueio real.

### 5. Suavizacao indevida

Evitar reduzir severidade de problema P0/P1 para preservar tom agradavel.

Problema critico deve ser declarado de forma direta.

---

## Padrao esperado

A resposta deve ser:

- direta;
- tecnicamente honesta;
- respeitosa;
- baseada em evidencia;
- economica em tokens;
- clara sobre incerteza;
- clara sobre risco;
- sem bajulacao;
- sem CTA artificial.

---

## Saidas oficiais

Use uma das saidas:

```txt
PASS
Reason:
Evidence:
```

```txt
TRIM_ENGAGEMENT
Reason:
Text to remove:
Neutral replacement:
```

```txt
REMOVE_SYCOPHANCY
Reason:
Text to remove:
Neutral replacement:
```

```txt
REWRITE_NEUTRAL
Reason:
Issues:
Neutral rewrite:
```

```txt
BLOCK_MISLEADING_AGREEMENT
Reason:
Unsupported agreement:
Risk:
Required correction:
```

---

## Posicao na governanca

Esta feature deve ser representada por artefatos existentes:

| Responsabilidade | Local recomendado |
|---|---|
| regra de comunicacao neutra | `rules/quality/neutral-technical-communication.md` |
| hook de validacao | `prompts/hooks/validate-neutrality-and-engagement.md` |
| eval de regressao | `evals/manual-regression-suite.md` |
| resultado de validacao | `evals/` |

Skill dedicada nao e obrigatoria no primeiro momento.

Nao criar novo diretorio para neutralidade.

---

## Relacao com features existentes

### Intake Governance

Intake valida se o pedido humano pode seguir.

Neutrality Governance valida se a resposta nao reforca premissa ruim por bajulacao ou concordancia indevida.

### Context Debt Audit

Context Debt Audit reduz custo e redundancia do repositorio.

Neutrality Governance reduz ruido e manipulacao social no texto produzido.

### Operational Safety

Safety bloqueia acao perigosa.

Neutrality Governance impede que risco seja suavizado por tom agradavel.

---

## Mudancas esperadas

### Obrigatorias para esta spec

- Criar `docs/remediation/neutrality-governance-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar

- Criar `rules/quality/neutral-technical-communication.md`.
- Criar `prompts/hooks/validate-neutrality-and-engagement.md`.
- Atualizar `governance/composition/context-composition.md` para reconhecer checkpoint sob demanda.
- Atualizar `README.md` e `INDEX.md` com explicacao curta.
- Adicionar eval manual com casos de bajulacao, concordancia indevida, CTA artificial e tom neutro aceitavel.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.
- Atualizar `governance/authoring/artifact-registry.md` se a feature virar artefato critico.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Definir anti-padroes | Governanca de qualidade | spec | Criterios objetivos | Bajulacao, concordancia e engajamento definidos |
| 2 | Criar rule | Qualidade | `rules/quality/` | Regra reutilizavel | Proibe sycophancy sem virar persona |
| 3 | Criar hook | PromptOps | `prompts/hooks/` | Checkpoint sob demanda | Produz saidas oficiais |
| 4 | Atualizar composition | Governanca | `governance/composition/context-composition.md` | Checkpoint selecionavel | Nao entra por padrao |
| 5 | Atualizar roteadores | Docs | `README.md`, `INDEX.md` | Discovery claro | Texto curto e sem duplicar spec |
| 6 | Adicionar eval | QA de IA | `evals/manual-regression-suite.md` | Regressao coberta | Casos cobrem bajulacao e tom neutro aceitavel |
| 7 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Gates rastreados | PASS somente com evidencia |

---

## Criterios de aceite

A feature esta pronta quando:

- existe regra clara contra bajulacao e concordancia performatica;
- existe regra clara contra flags artificiais de engajamento;
- existe excecao para pergunta necessaria e cordialidade minima;
- existe hook com saidas oficiais;
- a feature nao cria persona;
- a feature nao entra na composicao padrao;
- evals cobrem:
  - elogio generico;
  - concordancia indevida;
  - falsa seguranca;
  - pergunta final desnecessaria;
  - resposta neutra aceitavel.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Virar grosseria | Piora de usabilidade | Exigir respeito e utilidade |
| Bloquear pergunta necessaria | Perda de clareza | Permitir pergunta que remove bloqueio real |
| Virar estilo subjetivo | Baixa consistencia | Usar anti-padroes objetivos |
| Remover empatia operacional | Resposta fria em contexto sensivel | Permitir reconhecimento factual sem bajulacao |
| Suavizar risco critico | Decisao insegura | Bloquear misleading agreement e falsa seguranca |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Neutrality Governance aprovado como guardrail de comunicacao neutra, anti-bajulacao e higiene de engajamento
Restricao: nao vira persona, nao remove cordialidade minima e nao bloqueia perguntas necessarias
```

---

## Limites

Esta spec define governanca de neutralidade e higiene de engajamento.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../prompts/`, `../../evals/` ou controles externos de runtime.
