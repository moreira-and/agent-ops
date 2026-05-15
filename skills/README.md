# skills

## Tipo do artefato

discovery

## Finalidade

O diretório `skills/` armazena conhecimento operacional reutilizável para execução especializada em engenharia de dados.

`skills/` existe para enriquecer a execução com capacidade técnica reaproveitável.

Este diretório deve concentrar conteúdos como:

- procedimentos transversais de evolução do `agent-ops`
- procedimentos
- heurísticas
- estratégias
- técnicas reutilizáveis
- guias operacionais especializados

A norma de maior precedência continua sendo:

- `../MANIFEST.md`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/composition/context-composition.md`

---

## Quando usar

Consulte `skills/` quando precisar:

- adicionar conhecimento operacional à execução
- orientar como realizar um tipo de trabalho
- aplicar técnica reutilizável em múltiplos contextos
- complementar a atuação de um agente com capacidade especializada

---

## Quando não usar

Não use `skills/` como fonte primária para:

- persona de agente
- regra normativa estrutural
- regra primária de output
- template de solicitação

Esses conteúdos pertencem, respectivamente, a:

- `../agents/`
- `../governance/`
- `../rules/`
- `../prompts/`

---

## Responsabilidade desta pasta

`skills/` MUST conter conhecimento operacional reutilizável.

`skills/` MUST NOT conter governança estrutural, persona ou regra normativa primária.

---

## Limites

Este README roteia a seleção de capacidades operacionais.

Este README não substitui:

- skills específicas nos subdiretórios
- regras obrigatórias em `../rules/`
- perfis em `../agents/`
- prompts em `../prompts/`

---

## Estrutura interna alvo

```txt
skills/
├── README.md
├── grow-from-execution.md
├── ingestion/
├── transformation/
├── orchestration/
├── modeling/
├── quality/
└── review/
```

### `ingestion/`
Conhecimento reutilizável sobre ingestão.

### `grow-from-execution.md`
Skill transversal para destilar conhecimento de execução passada e propor artefatos reutilizáveis.

### `transformation/`
Conhecimento reutilizável sobre transformação.

### `orchestration/`
Conhecimento reutilizável sobre orquestração.

### `modeling/`
Conhecimento reutilizável sobre modelagem.

### `quality/`
Conhecimento reutilizável sobre testes e validação.

### `review/`
Conhecimento reutilizável sobre revisão técnica.

---

## Fronteiras

### Pode conter
- técnica operacional
- heurística de execução
- procedimento reaproveitável
- estratégia de resolução
- padrões práticos reutilizáveis

### Não pode conter
- perfil de agente
- regra estrutural
- regra normativa primária
- prompt de workflow

---

## Relação com os demais diretórios

- é governado por `../governance/`
- deve respeitar `../rules/`
- é referenciado por `../agents/`
- pode ser acionado por `../prompts/`

---

## Uso pelo agente

Ao consumir `skills/`, o agente deve:

- usar a skill como capacidade operacional
- respeitar as regras relacionadas
- não transformar heurística em norma sem base explícita
- preferir skills reutilizáveis em vez de embutir conhecimento técnico dentro de agentes ou prompts
