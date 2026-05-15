# prompts

## Tipo do artefato

discovery

## Finalidade

O diretório `prompts/` define pontos de entrada para tarefas, fluxos e solicitações dentro do `agent-ops`.

`prompts/` existe para iniciar, orientar e conduzir trabalho.

Este diretório deve concentrar artefatos como:

- prompts transversais de evolução do `agent-ops`
- prompts de geração
- prompts de revisão
- prompts de discovery
- prompts de planejamento
- checkpoints de validação em `./hooks/`

A norma de maior precedência continua sendo:

- `../MANIFEST.md`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/composition/context-composition.md`

---

## Quando usar

Consulte `prompts/` quando precisar:

- iniciar uma tarefa
- estruturar uma solicitação
- seguir um fluxo guiado
- conduzir revisão
- organizar discovery ou planejamento
- executar checkpoint de validação

---

## Quando não usar

Não use `prompts/` como fonte primária para:

- governança estrutural
- regra normativa de output
- skill operacional reutilizável
- definição de agente

Esses conteúdos pertencem, respectivamente, a:

- `../governance/`
- `../rules/`
- `../skills/`
- `../agents/`

---

## Responsabilidade desta pasta

`prompts/` MUST atuar como ponto de entrada operacional.

`prompts/` MUST NOT virar repositório genérico de contexto sem classificação.

---

## Limites

Este README roteia a seleção de prompts e hooks.

Este README não substitui:

- prompts específicos
- regras em `../rules/`
- skills em `../skills/`
- perfis em `../agents/`

---

## Estrutura interna alvo

```txt
prompts/
├── README.md
├── grow-from-execution.md
├── generation/
├── review/
├── discovery/
├── planning/
└── hooks/
```

### `generation/`
Prompts para gerar artefatos.

### `grow-from-execution.md`
Prompt transversal para executar o fluxo `grow` a partir de um `.md` de execução anterior.

### `review/`
Prompts para revisar artefatos existentes.

### `discovery/`
Prompts para descobrir contexto necessário.

### `planning/`
Prompts para planejar antes de executar.

### `hooks/`
Prompts de checkpoint e validação ao longo do fluxo.

---

## Fronteiras

### Pode conter
- template de solicitação
- fluxo guiado
- entrada operacional
- instrução de execução por tarefa
- checkpoint de validação

### Não pode conter
- regra estrutural primária
- regra normativa primária
- skill operacional extensa
- definição completa de persona

---

## Relação com os demais diretórios

- usa `../governance/` como base padrão
- pode acionar `../agents/`
- pode carregar `../rules/`
- pode carregar `../skills/`
- inclui `./hooks/` para checkpoints

---

## Uso pelo agente

Ao consumir `prompts/`, o agente deve:

- usar o prompt como ponto de entrada
- respeitar a ordem oficial de composição
- carregar apenas o contexto necessário
- acionar `./hooks/` quando houver necessidade de validação adicional

---

## Sobre `./hooks/`

`./hooks/` contém prompts de checkpoint e validação.

Esses artefatos devem ser usados para:

- validar aderência a `../governance/`
- validar aderência a `../rules/`
- revisar conformidade antes ou depois de execução

`./hooks/` MUST NOT conter scripts, automações ou hooks executáveis.
