# enforce-semantic-naming

## Tipo do artefato

prompt

## Finalidade

Definir ponto de entrada para enforcement semântico de convenções de naming em schemas, SQL models, DataFrames e transformações de dados.

---

## Quando usar

Use este prompt quando precisar:

- validar conformidade de naming em schema
- detectar violações de naming em código
- corrigir automaticamente violações óbvias
- revisar e sugerir renomeações
- auditar consistência semântica
- estruturar governance de naming em pipeline

---

## Quando não usar

Não use este prompt quando:

- a tarefa exigir desenho arquitetural
- a tarefa exigir implementação de transformação
- a tarefa exigir decisão de negócio

Consulte, nesses casos:

- `../../agents/data-architecture/solid-data-architect.md`
- `../../agents/data-engineering/solid-data-engineer.md`

---

## Dependências relacionadas

- `../../governance/composition/semantic-naming-governance.md`
- `../../agents/data-engineering/semantic-naming-enforcement-agent.md`
- `../../rules/naming/README.md`
- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Composição recomendada

### Base
- `../../MANIFEST.md`
- `../../governance/principles/core-principles.md`
- `../../governance/composition/context-composition.md`

### Governance
- `../../governance/composition/semantic-naming-governance.md`

### Agent
- `../../agents/data-engineering/semantic-naming-enforcement-agent.md`

### Rules
- `../../rules/naming/README.md` (roteador do conjunto de naming)
- `../../rules/naming/reference-units.md` (tabela de unidades)
- `../../rules/naming/reference-severity.md` (tabela de severidade)

### Skills
- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Instrução operacional

Ao usar este prompt, o agente SHOULD:

1. Carregar composição recomendada
2. Atuar como agente de enforcement semântico
3. Executar detecção de violações
4. Classificar por severidade
5. Separar auto-fix de revisão humana
6. Documentar racional técnico
7. Gerar relatório estruturado

---

## Entradas esperadas

O agente MUST receber:

- **schema**: SQL DDL, DataFrame schema, ou definição de modelo
- **scope**: Quais artefatos validar (colunas, variáveis, aliases, etc.)
- **context**: Contexto semântico (domínio, entidades, relacionamentos)

### Exemplo de entrada

```
Schema:
CREATE TABLE customers (
    cod_cliente INT,
    nome VARCHAR(255),
    peso DECIMAL(10,2),
    dt_criacao TIMESTAMP,
    ativo BOOLEAN
);

Scope: Todas as colunas

Contexto: Tabela de clientes em domínio de e-commerce
```

---

## Saídas esperadas

O agente MUST produzir:

1. **Detecção:** Lista de todas as violações encontradas
2. **Análise:** Classificação por tipo, severidade e risco
3. **Correção:** Auto-fixes aplicados + casos pendentes
4. **Relatório:** Estruturado e auditável

### Exemplo de saída

```json
{
  "violations_detected": 4,
  "auto_fixed": 2,
  "requires_review": 2,
  "blocked": 0,
  "details": [
    {
      "name": "cod_cliente",
      "violation": "format + abbreviation",
      "severity": "HIGH",
      "suggestion": "customer_id",
      "status": "AUTO_FIXED"
    },
    {
      "name": "peso",
      "violation": "missing_unit",
      "severity": "HIGH",
      "suggestion": "weight_kg (ou weight_lb?)",
      "status": "REQUIRES_REVIEW",
      "reason": "Unidade é ambígua"
    }
  ]
}
```

---

## Checkpoints de validação

Antes de concluir, o agente SHOULD validar:

- [ ] Todas as violações foram detectadas?
- [ ] Classificação de severidade está correta?
- [ ] Auto-fixes são determinísticos?
- [ ] Casos ambíguos foram sinalizados?
- [ ] Racional técnico foi documentado?
- [ ] Relatório é estruturado e auditável?

---

## Guardrails operacionais

### Guardrail 1: Não inventar semântica

Se unidade, tipo ou significado é ambíguo:

- NÃO auto-fix
- Sinalizar para revisão
- Sugerir alternativas

### Guardrail 2: Não quebrar contratos

Se rename pode quebrar:

- queries em produção
- APIs externas
- documentação
- linhagem de dados

Então: **NÃO auto-fix**

### Guardrail 3: Documentar racional

Toda renomeação MUST ser documentada com:

- nome anterior
- nome novo
- tipo de transformação
- risco avaliado
- razão técnica

### Guardrail 4: Exigir confirmação para ambiguidade

Se múltiplas interpretações são possíveis:

- Solicitar confirmação explícita
- Listar alternativas
- Documentar ambiguidade

### Guardrail 5: Bloquear renomeações perigosas

Se rename pode quebrar contrato externo:

- Bloquear auto-fix
- Sinalizar para revisão humana
- Explicar risco

---

## Exemplo de execução completa

### Input

```
Schema:
CREATE TABLE orders (
    id_order INT,
    fk_customer INT,
    vlr_total DECIMAL(10,2),
    data_criacao TIMESTAMP,
    ativo BOOLEAN
);

Scope: Todas as colunas

Contexto: Tabela de pedidos em domínio de e-commerce
```

### Execução

**Fase 1: Detecção**

```
Violações encontradas:
1. id_order: formato invertido
2. fk_customer: prefixo técnico
3. vlr_total: abreviação + unidade faltante
4. data_criacao: abreviação + idioma misto
5. ativo: booleano sem prefixo
```

**Fase 2: Análise**

```
id_order:
  - Tipo: formato invertido
  - Severidade: MEDIUM
  - Risco: BAIXO
  - Auto-fix: SIM
  - Sugestão: order_id

fk_customer:
  - Tipo: prefixo técnico
  - Severidade: HIGH
  - Risco: ALTO (pode quebrar referências)
  - Auto-fix: NÃO
  - Sugestão: customer_id
  - Razão: Requer validação de contrato externo

vlr_total:
  - Tipo: abreviação + unidade faltante
  - Severidade: HIGH
  - Risco: MÉDIO (unidade ambígua)
  - Auto-fix: NÃO
  - Sugestão: total_amount_brl (ou total_amount_usd?)
  - Razão: Unidade é ambígua

data_criacao:
  - Tipo: abreviação + idioma misto
  - Severidade: HIGH
  - Risco: BAIXO
  - Auto-fix: SIM
  - Sugestão: created_at

ativo:
  - Tipo: booleano sem prefixo
  - Severidade: MEDIUM
  - Risco: MÉDIO (tipo deve ser confirmado)
  - Auto-fix: CONDICIONAL
  - Sugestão: is_active
  - Razão: Requer confirmação de tipo BOOLEAN
```

**Fase 3: Correção**

```
Auto-fixes aplicados:
✓ id_order → order_id
✓ data_criacao → created_at

Casos pendentes de revisão:
⚠ fk_customer → customer_id (BLOQUEADO: risco alto)
⚠ vlr_total → total_amount_brl (PENDENTE: unidade ambígua)
⚠ ativo → is_active (PENDENTE: tipo deve ser confirmado)
```

**Fase 4: Relatório**

```json
{
  "schema": "orders",
  "violations_detected": 5,
  "auto_fixed": 2,
  "requires_review": 2,
  "blocked": 1,
  "summary": {
    "critical": 0,
    "high": 3,
    "medium": 2,
    "low": 0
  },
  "details": [
    {
      "name": "id_order",
      "violation": "format_inverted",
      "severity": "MEDIUM",
      "suggestion": "order_id",
      "status": "AUTO_FIXED",
      "risk": "LOW"
    },
    {
      "name": "fk_customer",
      "violation": "technical_prefix",
      "severity": "HIGH",
      "suggestion": "customer_id",
      "status": "BLOCKED",
      "risk": "HIGH",
      "reason": "Pode quebrar referências externas"
    },
    {
      "name": "vlr_total",
      "violation": "abbreviation + missing_unit",
      "severity": "HIGH",
      "suggestion": "total_amount_brl (ou total_amount_usd?)",
      "status": "REQUIRES_REVIEW",
      "risk": "MEDIUM",
      "reason": "Unidade é ambígua"
    },
    {
      "name": "data_criacao",
      "violation": "abbreviation + mixed_language",
      "severity": "HIGH",
      "suggestion": "created_at",
      "status": "AUTO_FIXED",
      "risk": "LOW"
    },
    {
      "name": "ativo",
      "violation": "boolean_without_prefix",
      "severity": "MEDIUM",
      "suggestion": "is_active",
      "status": "REQUIRES_REVIEW",
      "risk": "MEDIUM",
      "reason": "Tipo deve ser confirmado como BOOLEAN"
    }
  ]
}
```

---

## Limites

Este prompt define ponto de entrada para enforcement de naming.

Este prompt não substitui:

- política de naming
- regras específicas
- procedimentos de validação
- procedimentos de detecção
- procedimentos de auto-fix

---

## Relação com demais artefatos

- usa `../../governance/composition/semantic-naming-governance.md`
- usa `../../agents/data-engineering/semantic-naming-enforcement-agent.md`
- usa `../../rules/naming/README.md`
- usa `../../rules/naming/reference-units.md`
- usa `../../rules/naming/reference-severity.md`
- usa `../../skills/review/semantic-naming-validation.md`
- usa `../../skills/review/semantic-naming-detection.md`
- usa `../../skills/review/semantic-naming-autofix.md`
