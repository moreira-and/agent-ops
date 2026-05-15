# quality-rules

## Tipo do artefato

rule

## Finalidade

Definir critérios normativos de qualidade para artefatos produzidos por agentes.

---

## Quando usar

Use este arquivo quando precisar:

- revisar qualidade mínima de uma entrega
- validar consistência e completude
- reduzir risco de ambiguidade
- reforçar conformidade antes da conclusão

---

## Quando não usar

Não use este arquivo como fonte primária para:

- qualidade dos arquivos do próprio `agent-ops`
- arquitetura
- implementação
- naming

Consulte, respectivamente:

- `../../governance/quality/artifact-quality-standard.md`
- `../architecture/architecture-rules.md`
- `../coding/coding-rules.md`
- `../naming/README.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../../governance/quality/artifact-quality-standard.md`

---

## Normas

### 1. Clareza
A saída MUST ser compreensível para o público esperado.

### 2. Coerência
A saída MUST ser internamente consistente.

### 3. Completude suficiente
A saída MUST cobrir o objetivo proposto sem lacunas críticas silenciosas.

### 4. Baixa ambiguidade
A saída SHOULD minimizar interpretações concorrentes.

### 5. Rastreabilidade
Referências, dependências e decisões relevantes SHOULD ser rastreáveis quando aplicável.

### 6. Aderência normativa
A saída MUST respeitar as regras aplicáveis carregadas no contexto.

### 7. Proporcionalidade
A saída SHOULD ter nível de detalhe proporcional à tarefa, sem excesso nem omissão crítica.

### 8. Não alucinação estrutural
A saída MUST NOT inventar artefatos, dependências ou premissas estruturais sem base no contexto fornecido.

---

## Limites

Este arquivo define qualidade de output.

Este arquivo não substitui:

- critérios de qualidade do próprio repositório
- normas arquiteturais
- normas de implementação
- convenções de naming
