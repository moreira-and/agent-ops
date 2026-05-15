# transformation-design

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para desenho de transformação de dados.

---

## Quando usar

Use este arquivo quando precisar:

- estruturar etapas de transformação
- revisar separação de responsabilidades em processamento
- orientar clareza de entradas, regras e saídas
- reduzir complexidade acidental em fluxos de transformação

---

## Quando não usar

Não use esta skill como fonte primária para:

- regra normativa de output
- governança estrutural
- prompt de geração

Consulte, respectivamente:

- `../../rules/`
- `../../governance/`
- `../../prompts/generation/`

---

## Dependências relacionadas

- `../../rules/architecture/architecture-rules.md`
- `../../rules/coding/coding-rules.md`
- `../../rules/quality/quality-rules.md`

---

## Capacidade operacional

Ao desenhar transformação, a execução SHOULD considerar:

### 1. Entrada e saída explícitas
A transformação SHOULD deixar claro o que recebe e o que produz.

### 2. Responsabilidade delimitada
Cada etapa SHOULD possuir responsabilidade principal clara.

### 3. Encadeamento compreensível
O fluxo de transformação SHOULD ser legível e rastreável.

### 4. Regras relevantes evidentes
As regras de transformação SHOULD ser compreensíveis e verificáveis.

### 5. Complexidade controlada
O desenho SHOULD evitar etapas excessivamente densas ou multifuncionais.

### 6. Preparação para revisão
A transformação SHOULD ser organizada de modo que revisão técnica e validação sejam viáveis.

---

## Limites

Este arquivo descreve capacidade operacional de transformação.

Este arquivo não substitui:

- regras normativas de implementação
- regras arquiteturais
- regras de qualidade
