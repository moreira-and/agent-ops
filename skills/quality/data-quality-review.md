# data-quality-review

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para revisão de qualidade em artefatos e fluxos de dados.

---

## Quando usar

Use este arquivo quando precisar:

- revisar clareza e consistência
- organizar análise de qualidade
- orientar validações antes de concluir
- reduzir risco de lacunas silenciosas

---

## Quando não usar

Não use esta skill como fonte primária para:

- regra normativa de qualidade
- governança estrutural
- hook de validação

Consulte, respectivamente:

- `../../rules/quality/quality-rules.md`
- `../../governance/`
- `../../prompts/hooks/`

---

## Dependências relacionadas

- `../../rules/quality/quality-rules.md`
- `../../rules/generation/generation-guardrails.md`

---

## Capacidade operacional

Ao revisar qualidade, a execução SHOULD considerar:

### 1. Objetivo atendido
A entrega SHOULD responder ao objetivo proposto.

### 2. Clareza suficiente
A entrega SHOULD ser compreensível para o público esperado.

### 3. Coerência interna
As partes da solução SHOULD ser consistentes entre si.

### 4. Rastreabilidade útil
Decisões e dependências relevantes SHOULD ser identificáveis quando necessário.

### 5. Lacunas explicitadas
Pontos incertos SHOULD ser sinalizados, e não ocultados.

### 6. Proporcionalidade
A profundidade da revisão SHOULD ser compatível com o risco e o tipo de entrega.

---

## Limites

Este arquivo descreve capacidade operacional de revisão de qualidade.

Este arquivo não substitui:

- critérios normativos de qualidade
- guardrails normativos de geração
