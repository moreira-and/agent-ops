# rules

## Tipo do artefato

discovery

## Finalidade

O diretório `rules/` define as normas e restrições que governam a saída produzida pelos agentes.

`rules/` é a fonte primária para padrões de output.

Este diretório deve concentrar normas sobre:

- crescimento controlado de artefatos
- arquitetura
- implementação
- modelagem
- nomenclatura
- qualidade
- guardrails de geração

A norma de maior precedência continua sendo:

- `../MANIFEST.md`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/principles/core-principles.md`
- `../governance/composition/context-composition.md`

---

## Quando usar

Consulte `rules/` quando precisar:

- garantir aderência arquitetural
- padronizar implementação
- seguir convenções de naming
- aplicar padrões de modelagem
- validar qualidade obrigatória
- restringir comportamento de geração

---

## Quando não usar

Não use `rules/` como fonte primária para:

- governança do `agent-ops`
- definição de persona de agente
- skill operacional reutilizável
- prompt de tarefa

Esses conteúdos pertencem, respectivamente, a:

- `../governance/`
- `../agents/`
- `../skills/`
- `../prompts/`

---

## Responsabilidade desta pasta

`rules/` MUST governar a saída produzida pelos agentes.

`rules/` MUST NOT governar a estrutura e a evolução do diretório `agent-ops`.

---

## Limites

Este README roteia a seleção de normas de output.

Este README não substitui:

- regras específicas nos subdiretórios de `rules/`
- governança estrutural em `../governance/`
- skills operacionais em `../skills/`
- perfis de agente em `../agents/`

---

## Estrutura interna alvo

```txt
rules/
├── README.md
├── growth-artifact-quality.md
├── architecture/
├── coding/
├── modeling/
├── naming/
├── quality/
└── generation/
```

### `architecture/`
Normas arquiteturais.

### `growth-artifact-quality.md`
Regra transversal para qualidade de artefatos criados ou atualizados por grow.

### `coding/`
Normas de implementação.

### `modeling/`
Normas de modelagem de dados.

### `naming/`
Convenções de nomenclatura.

### `quality/`
Critérios obrigatórios de qualidade.

### `generation/`
Guardrails específicos para geração por agentes.

---

## Fronteiras

### Pode conter
- obrigatoriedades
- proibições
- restrições normativas
- critérios de conformidade
- padrões esperados de saída

### Não pode conter
- governança estrutural
- skill técnica extensa
- definição de agente
- template de solicitação

---

## Relação com os demais diretórios

- é governado por `../governance/`
- é referenciado por `../agents/`
- pode ser acionado por `../prompts/`
- pode ser validado por `../prompts/hooks/`

---

## Uso pelo agente

Ao consumir `rules/`, o agente deve:

- tratar normas como restrições de output
- distinguir obrigação de recomendação
- não reinterpretar regra estrutural como skill
- não copiar regras para outros artefatos quando uma referência por caminho for suficiente
