# technical-review

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para revisão técnica de artefatos e soluções no contexto de engenharia de dados.

---

## Quando usar

Use este arquivo quando precisar:

- revisar uma solução antes de concluir
- avaliar coerência técnica
- identificar excesso de complexidade
- verificar clareza estrutural
- apoiar revisão crítica de implementação ou desenho

---

## Quando não usar

Não use esta skill como fonte primária para:

- regra normativa
- hook de validação formal
- governança estrutural

Consulte, respectivamente:

- `../../rules/`
- `../../prompts/hooks/`
- `../../governance/`

---

## Dependências relacionadas

- `../../rules/architecture/architecture-rules.md`
- `../../rules/quality/quality-rules.md`
- `../../rules/generation/generation-guardrails.md`

---

## Capacidade operacional

Ao realizar revisão técnica, a execução SHOULD considerar:

### 1. Clareza estrutural
A solução SHOULD possuir organização compreensível.

### 2. Separação de responsabilidades
As partes SHOULD possuir limites coerentes.

### 3. Complexidade proporcional
A solução SHOULD evitar complexidade maior que a necessária.

### 4. Coerência entre partes
As decisões técnicas SHOULD ser consistentes entre si.

### 5. Aderência ao contexto
A solução SHOULD respeitar o escopo e as regras carregadas.

### 6. Problemas explicitados
Riscos, conflitos ou lacunas SHOULD ser explicitados de forma objetiva.

---

## Limites

Este arquivo descreve capacidade operacional de revisão técnica.

Este arquivo não substitui:

- regras normativas
- prompts de validação
- governança estrutural
