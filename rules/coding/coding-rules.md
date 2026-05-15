# coding-rules

## Tipo do artefato

rule

## Finalidade

Definir normas de implementação para artefatos gerados por agentes em engenharia de dados.

---

## Quando usar

Use este arquivo quando precisar:

- gerar código
- revisar legibilidade e organização
- restringir complexidade desnecessária
- reforçar práticas consistentes de implementação

---

## Quando não usar

Não use este arquivo como fonte primária para:

- arquitetura de alto nível
- modelagem de dados
- convenções de naming
- governança estrutural

Consulte, respectivamente:

- `../architecture/architecture-rules.md`
- `../modeling/modeling-rules.md`
- `../naming/README.md`
- `../../governance/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../architecture/architecture-rules.md`

---

## Normas

### 1. Clareza antes de esperteza
A implementação MUST priorizar clareza sobre soluções excessivamente compactas ou implícitas.

### 2. Estrutura previsível
O código SHOULD possuir estrutura previsível e navegável.

### 3. Complexidade contida
A implementação SHOULD evitar complexidade acidental e ramificações desnecessárias.

### 4. Responsabilidade por unidade
Cada unidade de implementação SHOULD possuir responsabilidade principal clara.

### 5. Tratamento explícito de falhas
Falhas relevantes SHOULD ser tratadas ou sinalizadas de forma explícita.

### 6. Reuso com critério
Reuso SHOULD ser aplicado quando reduzir duplicação real e melhorar manutenção.

### 7. Sem acoplamento implícito
Dependências importantes SHOULD ser explícitas.

### 8. Comentário com propósito
Comentários SHOULD explicar intenção, exceção ou decisão não óbvia, e SHOULD NOT compensar código confuso.

---

## Limites

Este arquivo define normas gerais de implementação.

Este arquivo não substitui:

- normas arquiteturais
- convenções de naming
- regras de modelagem
- critérios de qualidade
