# Spec: root INDEX.md para descoberta barata por LLM

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir a implementacao de um `INDEX.md` no root do repositorio para ajudar LLMs e humanos a encontrar arquivos com menor custo cognitivo e menor consumo de contexto.

O `INDEX.md` deve ser um roteador compacto de descoberta. Ele nao deve virar README paralelo, manifesto alternativo, catalogo enciclopedico ou fonte normativa primaria.

---

## Problema

Hoje a descoberta inicial pode depender de:

- `README.md` raiz, que e orientado a humano;
- varios `README.md` de subdiretorios;
- busca ampla por arquivos;
- leitura acidental de documentacao e exemplos fora do contexto operacional.

Isso aumenta risco de:

- carregar contexto demais;
- pagar tokens em explicacoes humanas;
- duplicar mapas em varios READMEs;
- drift entre documentacao e estrutura real;
- ferir a filosofia de ser barato.

---

## Objetivo

Criar `./INDEX.md` como indice seco para apoiar o fluxo:

```txt
find -> select -> inject
```

O arquivo deve permitir que uma LLM responda rapidamente:

- quais roteadores existem;
- por onde comecar para cada necessidade;
- quais diretorios sao injetaveis;
- quais diretorios sao documentais ou de validacao;
- quais arquivos nunca devem ser tratados como fonte primaria;
- quando consultar `docs/` ou `evals/`.

---

## Nao objetivos

Nao fazer nesta feature:

- substituir `./MANIFEST.md`;
- substituir `./README.md`;
- copiar conteudo de READMEs de subdiretorios;
- listar todos os arquivos do repositorio;
- incluir exemplos longos;
- incluir diagramas pesados;
- criar nova taxonomia;
- transformar `docs/` ou `evals/` em contexto padrao;
- criar automacao de indexacao.

---

## Posicao na governanca

`INDEX.md` deve ser governado como artefato raiz.

### Precedencia

Em caso de conflito:

1. `./MANIFEST.md`
2. `./governance/`
3. diretorio especializado aplicavel
4. `./README.md`
5. `./INDEX.md`

Motivo: `INDEX.md` e um mapa de descoberta. Ele nao define regra.

### Tipo recomendado

```txt
discovery / llm-index
```

### Status de injecao

`INDEX.md` MAY ser carregado no inicio de uma tarefa quando o agente ainda nao sabe quais roteadores usar.

`INDEX.md` MUST NOT ser carregado depois que o contexto especifico ja foi selecionado, salvo necessidade de reorientacao.

`INDEX.md` MUST NOT ser usado como fonte normativa primaria.

---

## Responsabilidade do INDEX.md

`INDEX.md` MUST:

- listar roteadores principais por caminho;
- indicar por onde comecar para necessidades comuns;
- diferenciar nucleo injetavel de documentacao humana e evals;
- apontar a fonte normativa correta;
- ser pequeno o suficiente para caber em contexto inicial barato;
- referenciar caminhos, nao copiar conteudo.

`INDEX.md` MUST NOT:

- explicar regras em detalhe;
- duplicar workflows completos do README;
- copiar tabelas normativas;
- listar arquivos folha sem necessidade;
- conter exemplos de execucao;
- conter historico de auditoria;
- conter criterios de eval detalhados;
- usar linguagem que pareca substituir `MANIFEST.md`.

---

## Estrutura recomendada do INDEX.md

```md
# INDEX

## Tipo do artefato

discovery / llm-index

## Finalidade

Roteador barato para descoberta inicial por LLM.

## Fonte normativa

- `./MANIFEST.md`

## Ordem de uso

1. Ler este indice somente para descobrir o ponto de partida.
2. Selecionar o roteador adequado.
3. Carregar apenas os artefatos necessarios.
4. Descartar este indice quando o contexto especifico estiver escolhido.

## Roteadores principais

| Necessidade | Comece por |
|---|---|
| entender contrato estrutural | `./MANIFEST.md` |
| entender uso humano geral | `./README.md` |
| compor contexto | `./governance/composition/context-composition.md` |
| escolher agente | `./agents/README.md` |
| escolher rule | `./rules/README.md` |
| escolher skill | `./skills/README.md` |
| escolher prompt | `./prompts/README.md` |
| executar checkpoint | `./prompts/hooks/README.md` |
| consultar documentacao humana | `./docs/README.md` |
| validar regressao | `./evals/README.md` |

## Nucleo injetavel

- `./governance/`
- `./agents/`
- `./rules/`
- `./skills/`
- `./prompts/`

## Fora da composicao padrao

- `./docs/`
- `./evals/`
- `./LICENSE`

## Limites

Este indice nao substitui normas, regras, prompts, skills ou READMEs locais.
```

---

## Arquivos impactados

### Obrigatorios

- `./INDEX.md`
- `./README.md`
- `./MANIFEST.md`
- `./governance/composition/context-composition.md`
- `./docs/remediation/audit-remediation-orchestration.md`

### Condicionais

- `./evals/manual-regression-suite.md`
- `./evals/v0.1-manual-results.md`
- READMEs com diagramas redundantes, se a equipe decidir reduzir custo visual.

---

## Mudancas esperadas

### `./INDEX.md`

Criar arquivo novo com o contrato acima.

### `./README.md`

Adicionar referencia curta:

- `INDEX.md` e o mapa barato para descoberta inicial por LLM;
- `README.md` permanece guia humano principal.

### `./MANIFEST.md`

Registrar `INDEX.md` como artefato raiz permitido e nao normativo.

Nao alterar a taxonomia do nucleo injetavel salvo se estritamente necessario.

### `./governance/composition/context-composition.md`

Definir quando `INDEX.md` pode ser carregado:

- permitido no inicio de discovery;
- proibido como contexto tecnico depois da selecao;
- nao substitui roteadores locais.

### `./docs/remediation/audit-remediation-orchestration.md`

Registrar nova remediacao para governar a feature.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Inventariar roteadores reais | Orquestrador | `README.md`, `MANIFEST.md`, READMEs de primeiro nivel | Lista curta de pontos de entrada | Nenhum caminho inventado |
| 2 | Criar `INDEX.md` compacto | PromptOps / Context engineer | `INDEX.md` | Roteador barato criado | Menos de 120 linhas e sem exemplos longos |
| 3 | Registrar governanca do indice | Governanca | `MANIFEST.md`, `governance/composition/context-composition.md` | INDEX tem status e limites claros | Fica claro que nao e fonte normativa |
| 4 | Atualizar documentacao humana | Docs | `README.md`, `docs/remediation/audit-remediation-orchestration.md` | Humanos sabem quando usar o indice | README diferencia README humano de INDEX para LLM |
| 5 | Ajustar token economy visual | Context engineer | READMEs com diagramas redundantes, se aprovado | Reduz ruído opcional | Diagramas ficam so onde agregam decisao |
| 6 | Atualizar eval minimo | QA de IA | `evals/manual-regression-suite.md` | Caso cobre uso correto do INDEX | Eval garante que INDEX nao vira contexto padrao sempre |
| 7 | Validar | Orquestrador | repo | Checks passam | `git diff --check`; nenhum README sem status; INDEX sem norma duplicada |

---

## Criterios de aceite

A feature esta pronta quando:

- `./INDEX.md` existe.
- `INDEX.md` tem tipo, finalidade, fonte normativa, roteadores, limites e status de injecao.
- `INDEX.md` nao duplica regra, skill, prompt ou workflow detalhado.
- `INDEX.md` referencia caminhos existentes.
- `MANIFEST.md` reconhece `INDEX.md` como artefato raiz permitido e nao normativo.
- `governance/composition/context-composition.md` define quando o indice pode ser carregado.
- `README.md` diferencia `INDEX.md` de README humano.
- `evals/` possui pelo menos um caso que valida que o indice ajuda discovery sem virar carregamento padrao.
- `git diff --check` passa.
- Nenhum diretorio versionado fica sem `README.md`.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| `INDEX.md` virar README duplicado | Mais tokens e drift | Limite de tamanho e proibicao de explicacoes longas |
| `INDEX.md` competir com `MANIFEST.md` | Conflito normativo | Precedencia explicita abaixo do README |
| Listar todos os arquivos | Custo alto e manutencao ruim | Listar roteadores, nao folhas |
| LLM carregar INDEX sempre | Custo recorrente | Permitir apenas no inicio de discovery |
| Diagramas continuarem redundantes | Custo humano e drift | Avaliar remocao de diagramas em diretorios folha |

---

## Pergunta de decisao

Antes de implementar, o orquestrador deve decidir:

- manter diagramas em todos os READMEs; ou
- reduzir diagramas para root, diretorios de primeiro nivel e diretorios com decisao real.

Recomendacao tecnica: reduzir diagramas redundantes em READMEs folha depois que `INDEX.md` existir.

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
INDEX.md aprovado como roteador barato de descoberta inicial
Restricao: nao normativo, nao enciclopedico e nao carregado por padrao apos selecao de contexto
```

---

## Limites

Esta spec orienta a implementacao de `INDEX.md`.

Ela nao substitui `../../MANIFEST.md`, `../../README.md`, `../../governance/` ou `../../evals/`.
