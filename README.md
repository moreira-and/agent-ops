# agent-ops

## Tipo do artefato

readme / discovery

## Finalidade

O `agent-ops` centraliza, em arquivos `.md`, o contexto necessário para operação de agentes em engenharia de dados.

Este diretório existe para permitir:

- descoberta clara de contexto
- seleção modular
- injeção previsível
- aderência normativa
- baixa duplicação
- redução de alucinação

O `agent-ops` segue o modelo:

**find -> select -> inject**

A norma de maior precedência deste diretório está em:

- `./MANIFEST.md`

Este README é um roteador de navegação. Ele orienta descoberta inicial, mas não substitui o contrato normativo de `./MANIFEST.md`.

---

## Quando usar

Use este README quando precisar:

- entender rapidamente a finalidade do módulo
- descobrir qual diretório consultar primeiro
- aplicar o fluxo `find -> select -> inject`
- confirmar que `docs/` não entra na composição padrão

---

## Quando não usar

Não use este README como fonte primária para:

- norma estrutural do módulo
- regras técnicas de output
- skills operacionais
- perfis de agente
- prompts de tarefa

Consulte, respectivamente:

- `./MANIFEST.md`
- `./rules/`
- `./skills/`
- `./agents/`
- `./prompts/`

---

## Dependências relacionadas

- `./MANIFEST.md`
- `./governance/composition/context-composition.md`

---

## Como navegar

O diretório está organizado por responsabilidade.

### `./governance/`
Regras sobre como o sistema `agent-ops` deve funcionar, crescer e se manter coerente.

Use quando precisar entender:

- estrutura do repositório
- composição de contexto
- critérios de criação e manutenção de arquivos
- padrões de autoria e qualidade

### `./agents/`
Perfis de agentes especializados, com missão, escopo, limites e dependências contextuais.

Use quando precisar escolher:

- qual agente deve atuar
- como ele pensa
- quais `rules/` e `skills/` ele tende a consumir

### `./rules/`
Normas para a saída produzida pelos agentes.

Use quando precisar garantir:

- aderência arquitetural
- convenções de implementação
- padrões de modelagem
- qualidade de output
- guardrails de geração

### `./skills/`
Conhecimento operacional reutilizável.

Use quando precisar enriquecer a execução com:

- técnicas
- heurísticas
- procedimentos
- capacidades especializadas

### `./prompts/`
Pontos de entrada para tarefas e fluxos.

Use quando precisar:

- iniciar uma tarefa
- seguir um workflow
- estruturar uma solicitação
- conduzir revisão ou planejamento

### `./prompts/hooks/`
Checkpoints de validação durante fluxos.

Use quando precisar:

- validar aderência a `rules/`
- validar aderência a `governance/`
- revisar conformidade antes ou depois de executar

---

## Ordem oficial de composição

A ordem oficial de composição de contexto é:

```txt
prompt -> governance -> agent -> rules -> skills
```

### Interpretação rápida
1. `prompt` inicia o trabalho
2. `governance` injeta a base padrão
3. `agent` define o perfil executor
4. `rules` define restrições de output
5. `skills` adiciona conhecimento operacional

`prompts/hooks/` pode ser acionado como checkpoint quando necessário.

---

## Estrutura atual

A pasta `./docs/` foi adicionada à estrutura para documentação apenas para leitura humana. Veja a seção "Pasta `./docs/`" abaixo para mais detalhes.

```txt
agent-ops/
├── LICENSE
├── MANIFEST.md
├── README.md
├── docs/
├── governance/
├── agents/
│   └── agentops-growth-architect.md
├── rules/
│   └── growth-artifact-quality.md
├── skills/
│   └── grow-from-execution.md
└── prompts/
    ├── grow-from-execution.md
    └── hooks/
        └── validate-growth-proposal.md
```

A estrutura detalhada e a árvore alvo v1 estão definidas em:

- `./MANIFEST.md`

---

## Regras de uso

- Todo conteúdo de contexto injetável deve ser `.md`
- `docs/` contém documentação humana e não deve ser injetado por padrão
- `LICENSE` é metadado do repositório e não faz parte da composição de contexto
- Dependências devem ser referenciadas por caminho
- Cada arquivo deve ter responsabilidade única
- Conteúdo não deve ser duplicado entre diretórios
- `governance/` governa o sistema de artefatos
- `rules/` governa a saída produzida pelos agentes

---

## Ideologia arquitetural

O `agent-ops` aplica princípios equivalentes a SOLID e injeção de dependências em Markdown.

Para detalhes, consulte:

- `./governance/principles/core-principles.md`
- `./governance/composition/context-composition.md`
- `./governance/lifecycle/artifact-lifecycle-policy.md`

---

## Limites

Este README define navegação inicial e critérios de descoberta.

Este README não define:

- precedência normativa além da referência a `./MANIFEST.md`
- regras técnicas de output
- procedimentos operacionais especializados
- conteúdo humano de `./docs/` como contexto padrão

---

## Pasta `./docs/`

A pasta `./docs/` contém documentação **apenas para leitura humana** sobre o projeto. Inclui guias práticos por problema e exemplos simples para desenvolvedores e operadores.

**Importante para agentes:** Esta pasta **NÃO deve ser injetada por padrão** durante a execução de tarefas. O agente deve consultar `./docs/` apenas quando a tarefa for explicitamente sobre documentação humana, integração ou orientação operacional; para composição padrão, deve trabalhar com `governance/`, `agents/`, `rules/`, `skills/` e `prompts/`.

---

## Quando consultar primeiro cada área

### Comece por `./MANIFEST.md` quando:
- precisar entender a norma geral do diretório
- houver dúvida de precedência
- precisar decidir onde um novo artefato pertence

### Comece por `./prompts/` quando:
- já houver uma tarefa ou solicitação concreta

### Comece por `./agents/` quando:
- precisar escolher o perfil executor adequado

### Comece por `./rules/` quando:
- precisar garantir aderência do output

### Comece por `./skills/` quando:
- precisar de capacidade operacional especializada

### Comece por `./governance/` quando:
- precisar manter, expandir ou revisar o próprio `agent-ops`

---

## Precedência normativa

Em caso de conflito interpretativo, a precedência é:

1. `./MANIFEST.md`
2. `./governance/`
3. diretório especializado aplicável
4. `README.md`

---

## Expectativa de comportamento do agente

Ao consumir este diretório, o agente deve:

- atuar como defensor da norma
- evitar duplicação
- respeitar responsabilidade única
- operar com composição seletiva
- sinalizar lacunas em vez de inventar contexto
- referenciar artefatos por caminho
