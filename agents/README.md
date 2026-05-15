# agents

## Tipo do artefato

discovery

## Finalidade

O diretório `agents/` define perfis de agentes especializados para atuação em engenharia de dados.

Cada agente descreve:

- missão
- escopo
- limites
- forma de atuação
- critérios de decisão
- dependências contextuais

Os agentes não são a fonte primária de regras nem de conhecimento operacional reutilizável.

A norma de maior precedência continua sendo:

- `../MANIFEST.md`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/composition/context-composition.md`

---

## Quando usar

Consulte `agents/` quando precisar:

- escolher qual agente deve atuar
- entender o escopo e os limites de um perfil
- decidir qual estilo de raciocínio é mais adequado
- identificar quais `rules/` e `skills/` devem ser carregadas

---

## Quando não usar

Não use `agents/` como fonte primária para:

- regras normativas de output
- skills técnicas detalhadas
- governança estrutural
- prompts de tarefa

Esses conteúdos pertencem, respectivamente, a:

- `../rules/`
- `../skills/`
- `../governance/`
- `../prompts/`

---

## Responsabilidade desta pasta

`agents/` MUST definir quem atua, onde atua e sob quais dependências contextuais deve operar.

`agents/` MUST referenciar suas dependências por caminho.

`agents/` MUST NOT duplicar conteúdo primário de `../rules/` ou `../skills/`.

---

## Limites

Este README roteia a seleção de perfis em `agents/`.

Este README não substitui:

- arquivos de agente específicos
- regras em `../rules/`
- skills em `../skills/`
- prompts em `../prompts/`

---

## Estrutura interna alvo

```txt
agents/
├── README.md
├── agentops-growth-architect.md
├── data-engineering/
└── data-architecture/
```

### `agentops-growth-architect.md`
Perfil transversal para evoluir o próprio `agent-ops` a partir de execuções anteriores.

### `data-engineering/`
Perfis orientados à execução de engenharia de dados.

Exemplos:
- engenheiro de dados SOLID
- especialista em pipelines
- engenheiro de transformação

### `data-architecture/`
Perfis orientados a desenho e decisão arquitetural.

Exemplos:
- arquiteto de dados SOLID
- arquiteto de pipelines
- especialista em modelagem estrutural

---

## Fronteiras

### Pode conter
- missão do agente
- escopo
- limites
- critérios de decisão
- estilo de pensamento
- referências para `../rules/`
- referências para `../skills/`
- referências para `../prompts/`, quando fizer sentido

### Não pode conter
- regra primária de output
- skill operacional primária
- governança estrutural
- workflow detalhado de solicitação

---

## Relação com os demais diretórios

- obedece `../governance/`
- referencia `../rules/`
- referencia `../skills/`
- pode ser acionado por `../prompts/`

---

## Uso pelo agente

Ao consumir um perfil em `agents/`, o agente deve:

- respeitar o escopo definido
- respeitar os limites declarados
- carregar regras e skills referenciadas
- não extrapolar sua missão sem sinalização explícita
