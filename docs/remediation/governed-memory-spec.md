# Spec: Governed Memory

## Tipo do artefato

human documentation / execution spec

## Finalidade

Definir como o conceito de `Governed Memory` deve ser introduzido no `agent-ops` sem virar memoria livre, historico bruto, regra fantasma ou contexto carregado por padrao.

Neste repositorio, memory deve significar:

```txt
contexto reutilizavel, estavel, pequeno, versionado e auditavel, selecionado sob demanda
```

Memory nao e lembranca automatica do agente.

---

## Problema

Agentes precisam de continuidade entre execucoes, mas memoria mal governada cria riscos maiores que o beneficio:

- obedecer historico antigo sem validacao;
- transformar preferencia informal em norma;
- carregar contexto demais por habito;
- misturar decisao aprovada com suposicao;
- reter dados sensiveis ou transitorios;
- criar acoplamento invisivel entre execucoes;
- competir com `MANIFEST.md`, `governance/`, `rules/`, `skills/`, `prompts/` ou `docs/`.

Sem governanca, `memories` vira um repositorio de notas soltas e aumenta alucinacao estrutural.

---

## Objetivo

Definir uma camada futura de memoria governada que:

- preserve `intake -> find -> select -> inject -> execute`;
- entre apenas como candidata durante `find`;
- seja opcional e seletiva;
- armazene apenas fatos estaveis e reutilizaveis;
- tenha criterio de entrada, revisao, expiracao e remocao;
- nao substitua fontes normativas;
- nao armazene historico bruto, segredo, dado pessoal ou suposicao.

---

## Nao objetivos

Nao fazer nesta feature:

- criar memoria automatica do agente;
- salvar conversa bruta;
- criar banco vetorial;
- criar runtime, plugin, automacao ou ferramenta;
- carregar memories por padrao;
- criar diretorio raiz antes de provar necessidade;
- duplicar `docs/`, `rules/`, `skills/`, `governance/` ou `MANIFEST.md`;
- registrar preferencias nao confirmadas;
- armazenar informacao sensivel, credenciais, segredos ou dados pessoais.

---

## Nome recomendado

Use o conceito:

```txt
Governed Memory
```

Nomes aceitaveis em texto explicativo:

- `governed memory`
- `memoria governada`
- `reusable operational context`

Evite:

- `agent memory` quando sugerir autonomia livre;
- `memories` sem qualificacao;
- `long-term memory` quando nao houver runtime real;
- `knowledge base` se competir com `docs/` ou `skills/`.

---

## Definicao operacional

Uma memory e um fato ou decisao que atende todos os criterios:

- e estavel o suficiente para ser reutilizado;
- foi aprovado ou tem origem rastreavel;
- reduz custo de contexto em mais de uma tarefa;
- nao pertence melhor a `MANIFEST.md`, `governance/`, `rules/`, `skills/`, `prompts/`, `docs/` ou `evals/`;
- pode ser expresso de forma curta;
- tem escopo, validade e limite claros;
- nao contem segredo, dado pessoal ou historico bruto.

Se qualquer criterio falhar, o conteudo MUST NOT virar memory.

---

## Posicao no fluxo

Governed Memory entra apenas como candidata em `find`:

```txt
intake -> find -> select -> inject -> execute
             ^
             |
       memories candidatas
```

Regras:

- memory MUST NOT ser carregada antes de intake;
- memory MUST NOT ser contexto padrao;
- memory MAY ser descoberta durante `find`;
- memory MAY ser selecionada quando for menor e mais precisa que carregar documentacao maior;
- memory MUST ser descartada se nao for relevante para a tarefa;
- memory MUST perder precedencia para fonte normativa primaria.

---

## Precedencia

Em caso de conflito, a precedencia deve ser:

1. `MANIFEST.md`
2. `governance/`
3. diretorio especializado aplicavel
4. `rules/`
5. `prompts/`
6. `skills/`
7. `README.md`
8. `INDEX.md`
9. Governed Memory

Motivo: memory e contexto auxiliar. Ela nunca define norma primaria.

---

## O que pode virar memory

Pode virar memory:

- decisao arquitetural aprovada e recorrente;
- preferencia estavel confirmada pelo maintainer;
- convencao local que nao justifica uma rule;
- restricao de projeto frequentemente reutilizada;
- fato de dominio pequeno e estavel;
- licao aprendida recorrente de execucoes;
- ponte curta para localizar fonte primaria.

Exemplo aceitavel:

```txt
O nome oficial do sistema e `agent-ops`; `prompt-ops` e categoria operacional/historica.
Fonte: ./MANIFEST.md
Status: approved
```

---

## O que nao pode virar memory

MUST NOT virar memory:

- conversa bruta;
- log de execucao;
- decisao temporaria;
- preferencia inferida;
- suposicao do agente;
- dado sensivel;
- credencial ou segredo;
- dado pessoal;
- conteudo regulatorio, juridico ou financeiro sem fonte primaria;
- regra que deveria estar em `rules/`;
- principio estrutural que deveria estar em `governance/`;
- procedimento que deveria estar em `skills/`;
- prompt ou workflow que deveria estar em `prompts/`;
- documentacao explicativa que deveria estar em `docs/`;
- eval ou resultado de validacao que deveria estar em `evals/`.

---

## Estrutura recomendada

Nao criar sem necessidade comprovada.

Se criada, a pasta recomendada e `_memory/`, nao `memory/`.

O prefixo `_` indica diretorio auxiliar governado, fora da composicao padrao e fora das categorias principais do nucleo operacional.

Regra de nomenclatura:

- `_memory/` SHOULD ser usado para memoria governada.
- `memory/` SHOULD NOT ser usado porque parece categoria operacional comum.
- `_` MUST NOT ser aplicado em massa a diretorios oficiais como `governance/`, `agents/`, `rules/`, `skills/` ou `prompts/`.
- `docs/` e `evals/` SHOULD permanecer sem `_` por serem convencoes reconhecidas e ja governadas como fora da composicao padrao.
- `_historical_prompts/` MAY ser usado se historico de prompts voltar a existir, pois historico nao deve parecer prompt atual.

Quando a feature for aprovada, a menor estrutura aceitavel e:

```txt
_memory/
├── README.md
├── project-decisions.md
├── stable-preferences.md
└── lessons-learned.md
```

### `_memory/README.md`

Roteia o diretorio, declara limites, status de injecao e precedencia.

### `project-decisions.md`

Decisoes aprovadas e estaveis que nao pertencem ao manifesto nem a governance.

### `stable-preferences.md`

Preferencias confirmadas e recorrentes de operacao ou estilo.

### `lessons-learned.md`

Licoes reutilizaveis derivadas de execucoes, sem historico bruto.

---

## Contrato minimo de uma memory

Cada item de memory MUST conter:

```txt
ID:
Status: proposed | approved | deprecated
Tipo: decision | preference | fact | lesson | locator
Escopo:
Conteudo:
Fonte:
Criado em:
Revisar em:
Expira em: none | data
Limites:
```

Regras:

- `Fonte` MUST apontar caminho, issue, decisao humana ou artefato rastreavel.
- `Conteudo` SHOULD ser curto.
- `Status: proposed` MUST NOT ser injetado como fato.
- `deprecated` MUST NOT ser usado para orientar execucao.

---

## Contrato de composicao

`governance/composition/context-composition.md` SHOULD declarar:

- memory e candidata apenas em `find`;
- memory nao entra por padrao;
- memory deve ter motivo explicito para selecao;
- memory perde para fonte primaria;
- memory deve ser descartada quando a fonte primaria especifica for carregada e suficiente.

---

## Contrato de criacao

Uma nova memory MAY ser proposta quando:

- o mesmo fato aparece em multiplas execucoes;
- a informacao e estavel;
- carregar a fonte completa e caro demais para tarefas comuns;
- a memory aponta para a fonte primaria em vez de duplica-la;
- a ausencia da memory aumenta risco real de erro.

Uma nova memory MUST NOT ser criada quando:

- a informacao ainda e incerta;
- o conteudo e sensivel;
- a informacao pertence a uma fonte primaria existente;
- o uso esperado e unico;
- a memory serve apenas para evitar ler o artefato correto.

---

## Mudancas esperadas para implementacao

### Obrigatorias

- Criar `docs/remediation/governed-memory-spec.md`.
- Registrar a spec em `docs/remediation/README.md`.

### Ao implementar `_memory/`

- Atualizar `MANIFEST.md` para reconhecer `_memory/` como diretorio auxiliar condicional e nao integrante do nucleo padrao.
- Atualizar `governance/composition/context-composition.md` para posicionar memories como candidatas em `find`.
- Criar `_memory/README.md`.
- Criar apenas os arquivos de memory estritamente necessarios.
- Atualizar `README.md` e `INDEX.md` com referencia curta.
- Adicionar eval manual em `evals/manual-regression-suite.md`.
- Registrar resultado em `evals/`.
- Registrar remediacao em `docs/remediation/audit-remediation-orchestration.md`.

---

## Plano de execucao

| Ordem | Acao | Responsavel sugerido | Arquivos impactados | Resultado esperado | Criterio de aceite |
|---|---|---|---|---|---|
| 1 | Inventariar necessidade real | Orquestrador | execucoes anteriores, docs, manifest | Lista curta de fatos recorrentes | Nenhum item sem fonte rastreavel |
| 2 | Classificar candidatos | Governanca | proposta de memory | Separar decision, preference, fact, lesson, locator | Cada candidato justifica por que nao pertence a outra pasta |
| 3 | Decidir criar ou nao `_memory/` | Orquestrador | `MANIFEST.md`, spec | Decisao explicita | Criar diretorio somente se houver pelo menos 3 memories aprovadas |
| 4 | Criar estrutura minima | Docs / Governanca | `_memory/README.md`, arquivos minimos | Memory roteavel e limitada | Nenhum historico bruto ou dado sensivel |
| 5 | Atualizar composicao | Maintainer | `governance/composition/context-composition.md` | Memory entra apenas em find | Nao vira contexto padrao |
| 6 | Atualizar roteadores | Docs | `README.md`, `INDEX.md` | Humanos e LLMs sabem quando consultar | Texto curto, sem duplicar conteudo |
| 7 | Adicionar evals | QA de IA | `evals/` | Casos cobrem uso e abuso | Testa conflito com fonte primaria e dado sensivel |
| 8 | Registrar remediacao | Orquestrador | `docs/remediation/audit-remediation-orchestration.md` | Feature rastreavel | Gates PASS/FAIL com evidencia |

---

## Criterios de aceite

A feature so pode ser implementada quando:

- houver necessidade recorrente demonstrada;
- houver pelo menos tres memories candidatas aprovadas;
- cada memory tiver fonte rastreavel;
- nenhuma memory duplicar fonte primaria;
- nenhuma memory contiver segredo, dado pessoal ou historico bruto;
- `_memory/` estiver fora da composicao padrao;
- o prefixo `_` estiver justificado como sinal de diretorio auxiliar, nao como nova categoria operacional;
- `governance/composition/context-composition.md` declarar memory como candidata apenas em `find`;
- `README.md` e `INDEX.md` deixarem claro que memory nao e normativa;
- `evals/` validar:
  - memory util selecionada sob demanda;
  - memory rejeitada por conflito com fonte primaria;
  - tentativa de salvar dado sensivel recusada;
  - memory nao carregada por padrao.

---

## Riscos

| Risco | Impacto | Mitigacao |
|---|---|---|
| Memory virar regra fantasma | Agente obedece conteudo sem autoridade | Precedencia abaixo de fontes primarias |
| Memory virar historico bruto | Alto custo e ruido | Proibir logs, conversas e execucoes completas |
| Memory guardar dado sensivel | Risco operacional e legal | Proibicao explicita e eval de recusa |
| Memory competir com docs ou skills | Duplicidade e drift | Exigir justificativa de nao pertencimento |
| Memory ser carregada sempre | Custo e acoplamento invisivel | Apenas candidata em `find`, nunca padrao |
| Memory envelhecer | Decisoes antigas orientam execucao | `Revisar em` e `Expira em` obrigatorios |

---

## Veredito esperado

Se implementado conforme esta spec:

```txt
Status: PASS
Governed Memory aprovada como contexto auxiliar, seletivo e auditavel
Restricao: nao automatica, nao normativa, nao sensivel e nao carregada por padrao
```

---

## Limites

Esta spec define o conceito e os criterios para Governed Memory.

Ela nao autoriza criar `_memory/` automaticamente.

Ela nao substitui `../../MANIFEST.md`, `../../governance/`, `../../rules/`, `../../skills/`, `../../prompts/`, `../../docs/` ou `../../evals/`.
