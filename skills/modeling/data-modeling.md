# data-modeling

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para desenho e revisão de modelagem de dados.

---

## Quando usar

Use este arquivo quando precisar:

- desenhar entidades e estruturas
- revisar coerência de modelagem
- orientar contratos de dados
- alinhar estrutura com uso esperado

---

## Quando não usar

Não use esta skill como fonte primária para:

- norma obrigatória de modelagem
- regra completa de naming
- critério normativo de qualidade

Consulte, respectivamente:

- `../../rules/modeling/modeling-rules.md`
- `../../rules/naming/README.md`
- `../../rules/quality/quality-rules.md`

---

## Dependências relacionadas

- `../../rules/modeling/modeling-rules.md`
- `../../rules/naming/_core-pattern.md`
- `../../rules/naming/README.md`
- `../../rules/quality/quality-rules.md`

---

## Capacidade operacional

Ao trabalhar com modelagem, a execução SHOULD considerar:

### 1. Semântica antes de conveniência
A estrutura SHOULD refletir significado e uso esperado dos dados.

### 2. Granularidade coerente
A granularidade SHOULD ser compatível com o objetivo do artefato.

### 3. Contratos compreensíveis
Entradas, saídas, campos e restrições SHOULD ser compreensíveis.

### 4. Estrutura revisável
A modelagem SHOULD permitir revisão sem exigir inferência excessiva.

### 5. Consistência entre entidades
Entidades relacionadas SHOULD preservar coerência conceitual.

### 6. Preparação para evolução
A modelagem SHOULD considerar evolução previsível sem instabilidade desnecessária.

---

## Limites

Este arquivo descreve capacidade operacional de modelagem.

Este arquivo não substitui:

- normas de modelagem
- convenções de naming
- critérios normativos de qualidade
