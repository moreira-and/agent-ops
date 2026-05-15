# ingestion-design

## Tipo do artefato

skill

## Finalidade

Definir conhecimento operacional reutilizável para desenho de ingestão de dados.

---

## Quando usar

Use este arquivo quando precisar:

- estruturar ingestão de dados
- organizar etapas de entrada
- revisar clareza do fluxo de ingestão
- orientar decisões operacionais de captura e carregamento

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
- `../../rules/quality/quality-rules.md`

---

## Capacidade operacional

Ao desenhar ingestão, a execução SHOULD considerar:

### 1. Origem claramente identificada
A origem dos dados SHOULD ser clara e rastreável.

### 2. Etapas explícitas
As etapas de captura, validação inicial e disponibilização SHOULD ser explícitas.

### 3. Limites do fluxo
O ponto de entrada e o ponto de saída da ingestão SHOULD ser compreensíveis.

### 4. Tratamento de falhas relevantes
Falhas relevantes SHOULD ser tratadas ou sinalizadas de forma explícita.

### 5. Evolução controlada
O desenho da ingestão SHOULD permitir adaptação a mudanças previsíveis de origem ou formato.

### 6. Acoplamento contido
A ingestão SHOULD evitar dependências desnecessárias com camadas posteriores.

---

## Limites

Este arquivo descreve capacidade operacional de ingestão.

Este arquivo não substitui:

- normas arquiteturais
- normas de qualidade
- regras de modelagem
