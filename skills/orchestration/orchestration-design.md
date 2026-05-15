# orchestration-design

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para desenho de orquestração em fluxos de dados.

---

## Quando usar

Use este arquivo quando precisar:

- organizar execução em múltiplas etapas
- desenhar dependências entre partes do fluxo
- revisar ordem, checkpoints e coordenação operacional
- orientar estruturação de fluxos orquestrados

---

## Quando não usar

Não use esta skill como fonte primária para:

- regra normativa de output
- governança estrutural
- prompt de planejamento

Consulte, respectivamente:

- `../../rules/`
- `../../governance/`
- `../../prompts/planning/`

---

## Dependências relacionadas

- `../../rules/architecture/architecture-rules.md`
- `../../rules/quality/quality-rules.md`

---

## Capacidade operacional

Ao desenhar orquestração, a execução SHOULD considerar:

### 1. Ordem explícita
A sequência de execução SHOULD ser compreensível.

### 2. Dependências claras
Dependências entre etapas SHOULD ser explícitas.

### 3. Checkpoints úteis
Pontos de validação SHOULD existir quando reduzirem risco operacional.

### 4. Isolamento de etapas
Etapas SHOULD manter responsabilidades distinguíveis.

### 5. Tratamento de falhas relevantes
Falhas relevantes SHOULD poder ser detectadas, tratadas ou sinalizadas.

### 6. Evolução sustentável
A orquestração SHOULD permitir ajuste incremental sem reestruturação ampla desnecessária.

---

## Limites

Este arquivo descreve capacidade operacional de orquestração.

Este arquivo não substitui:

- normas arquiteturais
- critérios normativos de qualidade
- prompts de workflow
