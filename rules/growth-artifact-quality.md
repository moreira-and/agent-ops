# growth-artifact-quality

## Tipo do artefato

rule

## Status de injeção

condicional

## Finalidade

Definir regras obrigatórias para artefatos criados ou atualizados pela capacidade `grow`.

---

## Quando usar

Use esta rule quando precisar:

- validar proposta de crescimento do `agent-ops`
- criar artefato derivado de execução anterior
- atualizar artefato existente a partir de conhecimento destilado
- impedir absorção bruta de histórico como contexto injetável

---

## Quando não usar

Não use esta rule como fonte primária para:

- procedimento de extração de conhecimento
- perfil executor de grow
- workflow de entrada do grow
- documentação humana

Consulte, respectivamente:

- `../skills/grow-from-execution.md`
- `../agents/agentops-growth-architect.md`
- `../prompts/grow-from-execution.md`
- `../docs/`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/principles/core-principles.md`
- `../governance/lifecycle/artifact-lifecycle-policy.md`
- `../governance/quality/artifact-quality-standard.md`

---

## Precedência

Esta rule governa a qualidade de output do fluxo `grow`.

Ela não substitui `../MANIFEST.md` nem `../governance/`.

---

## Regras obrigatórias

### 1. Evidência obrigatória
Todo artefato criado ou atualizado por grow MUST estar sustentado por evidência no `.md` de execução analisado.

### 2. Destilação obrigatória
O fluxo grow MUST destilar conhecimento reutilizável.

Ele MUST NOT copiar o conteúdo bruto da execução.

### 3. Responsabilidade única
Cada artefato criado ou atualizado MUST manter uma única responsabilidade contextual.

### 4. Classificação correta
O conhecimento MUST ser classificado como prompt, agent, rule, skill, hook, governance, docs ou rejeição antes de qualquer alteração.

### 5. Recorrência mínima
Conhecimento pontual MUST NOT virar artefato injetável sem justificativa de recorrência.

### 6. Ausência de duplicação
O fluxo grow MUST verificar artefatos existentes antes de criar novo arquivo.

Conhecimento equivalente MUST atualizar ou referenciar fonte primária existente.

### 7. Compatibilidade com modelos simples
Artefatos derivados de grow MUST usar instruções curtas, explícitas e independentes de fornecedor.

### 8. Token economy
O grow MUST reduzir ambiguidade sem aumentar contexto obrigatório por padrão.

### 9. Dependências explícitas
Toda dependência contextual relevante MUST ser declarada por caminho.

### 10. Precedência normativa
O grow MUST preservar:

1. `../MANIFEST.md`
2. `../governance/`
3. diretório especializado aplicável
4. `../README.md`

### 11. Proibição de absorção indevida
Prompts MUST NOT absorver regras.

Agents MUST NOT absorver skills.

Skills MUST NOT virar normas obrigatórias.

Rules MUST NOT virar tutoriais operacionais.

Governance MUST NOT virar regra técnica de output.

Docs MUST NOT virar contexto injetável padrão.

---

## Critérios de rejeição

O grow MUST rejeitar conhecimento quando ele for:

- contexto bruto de execução
- específico demais para uma única ocorrência
- sem evidência suficiente
- duplicado por artefato existente
- dependente de vendor, modelo ou framework
- opinião sem generalização
- exemplo sem ganho operacional
- incompatível com `find -> select -> inject`

---

## Limites

Esta rule define qualidade obrigatória para artefatos derivados de grow.

Esta rule não define:

- procedimento operacional completo
- perfil executor
- prompt de entrada
- checkpoint de validação
