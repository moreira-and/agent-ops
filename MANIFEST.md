# MANIFEST.md

## Tipo do artefato

manifest

## Finalidade

Este manifesto define a norma estrutural e arquitetural do diretório `agent-ops`.

O `agent-ops` existe para organizar, em arquivos Markdown (`.md`), o contexto necessário para operação de agentes em engenharia de dados com:

- seleção modular de contexto
- forte aderência normativa
- mínima duplicação
- baixa ambiguidade
- redução de alucinação

Este arquivo é a norma de maior precedência do diretório.

---

## Quando usar

Use este manifesto quando precisar:

- resolver conflito normativo
- validar estrutura do módulo
- decidir onde um artefato pertence
- confirmar contrato de composição e precedência

## Quando não usar

Não use este manifesto como fonte primária para:

- regra técnica de output
- procedimento operacional especializado
- perfil executor
- prompt de tarefa

Consulte, respectivamente:

- `rules/`
- `skills/`
- `agents/`
- `prompts/`

## Dependências relacionadas

Este arquivo não depende de outro artefato interno.

Ele é a raiz normativa do `agent-ops`.

---

## 2. Escopo

O núcleo injetável do `agent-ops` é composto por arquivos `.md` em:

- `governance/`
- `agents/`
- `rules/`
- `skills/`
- `prompts/`

Esses diretórios MUST conter apenas arquivos `.md` destinados à injeção seletiva de contexto.

O repositório MAY conter metadados essenciais fora do núcleo injetável, como `LICENSE`.

O repositório MAY conter documentação humana em `docs/`, desde que ela não seja tratada como contexto injetável padrão.

O núcleo injetável MUST NOT conter:

- executáveis
- scripts
- hooks Git reais
- código de aplicação
- binários
- automações
- configurações operacionais externas ao contexto

Se um artefato não for contexto injetável em Markdown, ele MUST NOT existir nos diretórios do núcleo injetável.

---

## 3. Modelo operacional

O diretório MUST suportar o fluxo:

**find -> select -> inject**

Onde:

- **find** = descobrir contexto disponível
- **select** = escolher apenas o contexto relevante
- **inject** = carregar apenas o contexto necessário

O `agent-ops` MUST ser projetado para injeção seletiva.

O `agent-ops` MUST NOT depender de carregamento massivo por padrão.

---

## 4. Princípios normativos

### 4.1 Responsabilidade única
Cada arquivo `.md` MUST possuir uma responsabilidade principal clara.

Se um arquivo concentrar múltiplas responsabilidades centrais, ele SHOULD ser dividido.

### 4.2 Fonte primária única
Cada tipo de informação MUST possuir uma única fonte primária.

Arquivos secundários MAY referenciar essa fonte, mas MUST NOT competir com ela.

### 4.3 Mínima injeção necessária
Somente contexto necessário MUST ser carregado.

Contexto opcional MUST ser injetado apenas por relevância.

### 4.4 Referência por caminho
Toda dependência entre arquivos MUST ser expressa por caminho.

### 4.5 Não duplicação
O repositório MUST crescer por decomposição e referência.

O repositório MUST NOT crescer por cópia de conteúdo entre arquivos.

### 4.6 Clareza de obrigatoriedade
Artefatos SHOULD deixar claro se são:

- base padrão
- obrigatórios em contexto específico
- condicionais
- especializados

### 4.7 Crescimento controlado
A estrutura SHOULD evoluir apenas quando a mudança melhorar pelo menos um dos seguintes:

- recuperação
- seleção
- governança
- manutenção
- clareza
- controle de alucinação

### 4.8 SOLID e injeção de dependências em Markdown
O `agent-ops` MUST aplicar uma ideologia equivalente a SOLID e injeção de dependências adaptada a artefatos Markdown.

Isso significa:

- responsabilidade única para cada `.md`
- extensão por novos artefatos especializados, sem reescrita estrutural desnecessária
- substituição previsível entre artefatos da mesma categoria
- segregação de contexto para evitar carregamento desnecessário
- dependências explícitas por caminho
- injeção seletiva via `find -> select -> inject`

A fonte primária detalhada desse princípio é:

- `governance/principles/core-principles.md`

---

## 5. Taxonomia oficial

Todo arquivo SHOULD ser classificável em exatamente uma categoria principal:

- discovery
- governance
- agent
- rule
- skill
- prompt
- hook prompt

Se um arquivo não puder ser claramente classificado, ele SHOULD ser refatorado ou dividido.

Arquivos em `docs/` são documentação humana e não integram esta taxonomia de contexto injetável.

---

## 6. Estrutura oficial v1

```txt
agent-ops/
├── LICENSE
├── MANIFEST.md
├── README.md
├── docs/
├── governance/
│   ├── README.md
│   ├── principles/
│   ├── composition/
│   ├── authoring/
│   ├── lifecycle/
│   └── quality/
├── agents/
│   ├── README.md
│   ├── agentops-growth-architect.md
│   ├── data-engineering/
│   └── data-architecture/
├── rules/
│   ├── README.md
│   ├── growth-artifact-quality.md
│   ├── architecture/
│   ├── coding/
│   ├── modeling/
│   ├── naming/
│   ├── quality/
│   └── generation/
├── skills/
│   ├── README.md
│   ├── grow-from-execution.md
│   ├── ingestion/
│   ├── transformation/
│   ├── orchestration/
│   ├── modeling/
│   ├── quality/
│   └── review/
└── prompts/
    ├── README.md
    ├── grow-from-execution.md
    ├── generation/
    ├── review/
    ├── discovery/
    ├── planning/
    └── hooks/
```

Mudanças nessa estrutura MAY ocorrer, desde que preservem este manifesto.

---

## 7. Responsabilidades por diretório

### 7.1 `MANIFEST.md`
Define a norma-mãe do `agent-ops`.

### 7.2 `README.md`
Atua como roteador principal de navegação.

### 7.3 `governance/`
Define regras sobre estrutura, evolução, composição, autoria, qualidade e lifecycle do `agent-ops`.

`governance/` MUST governar o sistema de artefatos.

`governance/` MUST NOT definir regra técnica primária de saída.

### 7.4 `agents/`
Define perfis de agentes, seu escopo, limites, forma de atuação e dependências contextuais.

`agents/` MUST referenciar `rules/` e `skills/` por caminho quando aplicável.

`agents/` MUST NOT duplicar `rules/` ou `skills/`.

### 7.5 `rules/`
Define normas para a saída produzida pelos agentes.

`rules/` MUST governar output.

`rules/` MUST NOT governar a estrutura do `agent-ops`.

### 7.6 `skills/`
Define conhecimento operacional reutilizável.

`skills/` MUST conter capacidade reaproveitável.

`skills/` MUST NOT conter persona, workflow primário ou governança estrutural.

### 7.7 `prompts/`
Define pontos de entrada para tarefas, fluxos e solicitações.

`prompts/` MUST iniciar ou conduzir trabalho.

`prompts/` MUST NOT virar repositório genérico de contexto sem classificação.

### 7.8 `prompts/hooks/`
Define prompts de checkpoint e validação durante fluxos.

`prompts/hooks/` MUST validar aderência a `governance/` e/ou `rules/` quando aplicável.

`prompts/hooks/` MUST NOT conter hooks executáveis.

---

## 8. Ordem oficial de composição

A ordem oficial de composição é:

```txt
prompt -> governance -> agent -> rules -> skills
```

Interpretação:

1. `prompt` inicia a tarefa
2. `governance` injeta a base padrão
3. `agent` define o perfil executor
4. `rules` impõe as restrições de output
5. `skills` acrescenta conhecimento operacional

`prompts/hooks/` MAY ser acionado como checkpoint ao longo do fluxo.

`prompts/hooks/` NÃO integra a base obrigatória padrão.

---

## 9. Contrato mínimo de cada arquivo `.md`

Todo arquivo `.md` SHOULD explicitar, de forma clara:

- título
- tipo de artefato
- status de injeção, quando aplicável
- propósito
- escopo
- quando usar
- quando não usar
- dependências por caminho, se houver
- artefatos relacionados, quando aplicável
- precedência, quando aplicável
- limites
- instrução operacional, quando aplicável
- saídas esperadas, quando aplicável

Arquivos normativos SHOULD preferir linguagem:

- MUST
- MUST NOT
- SHOULD
- SHOULD NOT
- MAY

---

## 10. Contrato mínimo por categoria

### 10.1 Discovery
Deve informar:

- o que existe
- quando consultar
- o que é obrigatório
- o que é condicional

### 10.2 Governance
Deve informar:

- qual regra estrutural define
- onde ela se aplica
- o que obriga
- o que proíbe

### 10.3 Agent
Deve informar:

- missão
- escopo
- limites
- regras aplicáveis
- skills recomendadas

### 10.4 Rule
Deve informar:

- qual norma define
- a que se aplica
- o que é obrigatório
- o que é proibido

### 10.5 Skill
Deve informar:

- qual capacidade provê
- quando usar
- pré-condições
- limites
- regras relacionadas

### 10.6 Prompt
Deve informar:

- objetivo
- entradas esperadas
- composição recomendada
- saídas esperadas
- checkpoints recomendados

### 10.7 Hook Prompt
Deve informar:

- momento de uso
- o que valida
- contra quais normas valida
- ação em caso de não conformidade

---

## 11. Regras de decomposição

### 11.1 Criar novo arquivo
Um novo arquivo SHOULD ser criado quando houver:

- nova responsabilidade clara
- reutilização em múltiplos contextos
- ganho de precisão de recuperação
- redução de ambiguidade

### 11.2 Dividir arquivo existente
Um arquivo SHOULD ser dividido quando:

- concentrar múltiplas responsabilidades
- misturar norma e execução
- misturar identidade e capacidade
- misturar descoberta e conteúdo primário
- passar a atender múltiplos fluxos distintos

### 11.3 Não criar novo arquivo
Um novo arquivo SHOULD NOT ser criado quando:

- a separação for apenas cosmética
- não houver autonomia semântica
- a fragmentação piorar navegação
- não houver ganho de recuperação ou controle

### 11.4 Extrair fonte primária
Conteúdo repetido em múltiplos arquivos MUST ser extraído para uma fonte primária.

Os demais arquivos MUST passar a referenciá-la por caminho.

### 11.5 Evoluir sem quebrar composição
Novos conhecimentos SHOULD ser adicionados como artefatos plugáveis.

Mudanças em arquivos centrais SHOULD ocorrer apenas quando preservarem o contrato `find -> select -> inject`.

Prompts MUST NOT embutir regras indevidas.

Agents MUST NOT embutir skills indevidas.

Skills MUST NOT virar normas obrigatórias.

Rules MUST NOT virar tutoriais operacionais.

Governance MUST NOT virar regra técnica de output.

---

## 12. Guardrails anti-alucinação

O agente que consumir `agent-ops` MUST:

- não inferir estrutura inexistente
- não inventar caminhos ausentes
- não preencher lacunas silenciosamente
- não promover recomendação a norma sem base explícita
- não duplicar conteúdo para “facilitar”
- respeitar limites declarados de cada artefato

Se houver conflito, a precedência normativa é:

1. `MANIFEST.md`
2. `governance/`
3. diretório especializado aplicável
4. `README.md`

Se faltar contexto crítico, o agente SHOULD explicitar a lacuna.

---

## 13. Anti-patterns proibidos

São proibidos:

- arquivo enciclopédico
- prompt dumping
- regra duplicada
- skill normativa
- governance técnica de output
- agente autossuficiente por cópia
- fragmentação excessiva
- contexto especializado sempre carregado sem critério
- dependência contextual implícita
- acoplamento forte entre artefatos `.md`
- leitura indiscriminada do repositório como estratégia padrão

---

## 14. Comportamento esperado do agente

Ao consumir este manifesto, o agente MUST atuar como:

- defensor da norma
- implementador no padrão
- preservador da separação de responsabilidades
- evitador de duplicação
- executor de composição seletiva
- redutor de ambiguidade

Ao propor mudanças, o agente MUST:

1. identificar a responsabilidade primária do artefato
2. validar o diretório correto
3. verificar existência de fonte primária
4. evitar sobreposição
5. referenciar dependências por caminho
6. respeitar a ordem oficial de composição
7. validar baixo acoplamento e alta coesão
8. sinalizar lacunas antes de inventar conteúdo

---

## 15. Critério final de qualidade

Um artefato do `agent-ops` é de boa qualidade quando:

- possui responsabilidade única
- é classificável na taxonomia oficial
- informa propósito e limites
- referencia dependências por caminho
- mantém baixo acoplamento e alta coesão
- é compatível com injeção seletiva
- não duplica fonte primária
- melhora a seleção de contexto
- reduz ambiguidade
- aumenta precisão operacional

Artefatos que não atendam esses critérios SHOULD ser revistos, divididos, movidos ou removidos.

---

## Limites

Este manifesto define contrato estrutural, precedência e composição.

Este manifesto não substitui:

- regras especializadas em `rules/`
- capacidades operacionais em `skills/`
- perfis executores em `agents/`
- pontos de entrada em `prompts/`
