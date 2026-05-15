# architecture-rules

## Tipo do artefato

rule

## Finalidade

Definir normas arquiteturais para artefatos produzidos por agentes no contexto de engenharia de dados.

---

## Quando usar

Use este arquivo quando precisar:

- gerar soluções com separação clara de responsabilidades
- revisar desenho arquitetural
- orientar composição de componentes
- evitar acoplamento excessivo
- reforçar princípios SOLID adaptados ao domínio de dados

---

## Quando não usar

Não use este arquivo como fonte primária para:

- governança do `agent-ops`
- implementação de baixo nível
- convenções de naming
- procedimento operacional

Consulte, respectivamente:

- `../../governance/`
- `../coding/coding-rules.md`
- `../naming/README.md`
- `../../skills/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/principles/core-principles.md`

---

## Normas

### 1. Separação de responsabilidades
A solução MUST possuir separação clara de responsabilidades entre componentes.

### 2. Baixo acoplamento
Componentes MUST evitar dependências desnecessárias e acoplamento excessivo.

### 3. Alta coesão
Cada componente SHOULD concentrar uma responsabilidade principal coerente.

### 4. Composição explícita
Fluxos, módulos e etapas SHOULD possuir composição explícita e rastreável.

### 5. Extensibilidade controlada
A solução SHOULD permitir evolução incremental sem exigir reestruturação ampla para mudanças locais previsíveis.

### 6. Limites claros
Entradas, saídas e responsabilidades de cada parte MUST ser compreensíveis.

### 7. Reuso por abstração útil
Reuso SHOULD ocorrer quando aumentar consistência e manutenção, e SHOULD NOT introduzir abstração artificial.

### 8. Aderência ao domínio de dados
A arquitetura MUST refletir o fluxo real de ingestão, transformação, modelagem, validação e consumo quando aplicável.

---

## Limites

Este arquivo define normas arquiteturais gerais.

Este arquivo não substitui:

- regras de implementação
- regras de modelagem
- convenções de naming
- critérios de qualidade
