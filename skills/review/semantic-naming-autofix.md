# semantic-naming-autofix

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento operacional para corrigir automaticamente violações óbvias de naming semântico, com guardrails explícitos para casos ambíguos.

Este arquivo é a fonte primária para técnica de correção automática de naming.

---

## Quando usar

Use esta skill quando precisar:

- corrigir violações óbvias de naming
- aplicar transformações determinísticas
- gerar sugestões de renomeação
- estruturar auto-fix em pipeline
- documentar racional de correção

---

## Quando não usar

Não use esta skill como fonte primária para:

- política de naming
- regras específicas
- validação
- detecção
- prompts de enforcement

Consulte, respectivamente:

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `./semantic-naming-validation.md`
- `./semantic-naming-detection.md`
- `../../prompts/review/enforce-semantic-naming.md`

---

## Dependências relacionadas

- `../../rules/naming/README.md` (roteador do conjunto de naming)
- `../../governance/composition/semantic-naming-governance.md`
- `./semantic-naming-detection.md`

---

## Princípio de auto-fix

**Auto-fix é permitido apenas para transformações determinísticas e de baixo risco.**

**Auto-fix é bloqueado quando:**

- ambiguidade semântica existe
- múltiplas interpretações são possíveis
- rename pode quebrar contrato externo
- contexto de negócio é necessário

---

## Transformações permitidas (auto-fix)

### Transformação 1: camelCase → snake_case

**Condição:** Violação óbvia de formato

**Transformação:**
```
customerId → customer_id
productName → product_name
invoiceTotal → invoice_total
```

**Risco:** BAIXO

**Auto-fix:** SIM

---

### Transformação 2: Normalizar casing

**Condição:** Maiúsculas em nomes

**Transformação:**
```
Customer_ID → customer_id
PRODUCT_NAME → product_name
Invoice_Total → invoice_total
```

**Risco:** BAIXO

**Auto-fix:** SIM

---

### Transformação 3: Remover acentos

**Condição:** Acentos em nomes

**Transformação:**
```
cliente_código → cliente_codigo
produto_descrição → produto_descricao
endereço_rua → endereco_rua
```

**Risco:** BAIXO

**Auto-fix:** SIM

---

### Transformação 4: Substituir abreviações óbvias

**Condição:** Abreviação proibida com significado claro

**Transformação:**
```
cod_cliente → customer_code
vlr_total → total_amount
qtd_items → item_quantity
desc_produto → product_description
```

**Risco:** MÉDIO (requer contexto)

**Auto-fix:** CONDICIONAL

**Condição para auto-fix:**
- Abreviação é universalmente reconhecida
- Contexto semântico é claro
- Não há ambiguidade

---

### Transformação 5: Adicionar unidades óbvias

**Condição:** Valor mensurável sem unidade, contexto claro

**Transformação:**
```
weight → weight_kg (se contexto é claramente kg)
temperature → temperature_celsius (se contexto é claramente Celsius)
amount → amount_brl (se contexto é claramente BRL)
```

**Risco:** ALTO (requer confirmação)

**Auto-fix:** NÃO

**Razão:** Unidade pode ser ambígua (weight pode ser kg, lb, oz)

---

### Transformação 6: Remover sufixos de tipo

**Condição:** Tipo codificado em nome

**Transformação:**
```
customer_id_int → customer_id
amount_float → amount
name_string → name
is_active_boolean → is_active
```

**Risco:** BAIXO

**Auto-fix:** SIM

---

### Transformação 7: Adicionar prefixo a booleanos

**Condição:** Coluna booleana sem `is_` ou `has_`

**Transformação:**
```
active → is_active
deleted → is_deleted
primary → is_primary
address → has_address
```

**Risco:** MÉDIO (requer confirmação de tipo)

**Auto-fix:** CONDICIONAL

**Condição para auto-fix:**
- Tipo de dado é explicitamente BOOLEAN
- Semântica é clara

---

### Transformação 8: Adicionar sufixo a datas

**Condição:** Coluna de data sem `_date` ou `_at`

**Transformação:**
```
created → created_at
updated → updated_at
birth → birth_date
```

**Risco:** MÉDIO (requer confirmação de tipo)

**Auto-fix:** CONDICIONAL

**Condição para auto-fix:**
- Tipo de dado é explicitamente DATE ou TIMESTAMP
- Semântica é clara

---

### Transformação 9: Padronizar chaves estrangeiras

**Condição:** Chave estrangeira com prefixo técnico

**Transformação:**
```
fk_customer → customer_id
id_customer → customer_id
fk_product → product_id
```

**Risco:** ALTO (pode quebrar referências)

**Auto-fix:** NÃO

**Razão:** Requer validação de contrato externo

---

### Transformação 10: Remover double underscores

**Condição:** Underscores duplicados

**Transformação:**
```
customer__id → customer_id
product__name → product_name
```

**Risco:** BAIXO

**Auto-fix:** SIM

---

## Algoritmo de auto-fix

```
Para cada violação detectada:
    
    1. Classificar tipo de transformação
    2. Verificar se transformação está em lista de auto-fix permitido
    3. Se SIM:
        - Aplicar transformação
        - Documentar mudança
        - Adicionar a relatório
    4. Se CONDICIONAL:
        - Verificar condições
        - Se todas as condições são atendidas:
            - Aplicar transformação
            - Documentar mudança
        - Senão:
            - Sinalizar para revisão humana
    5. Se NÃO:
        - Sinalizar para revisão humana
        - Sugerir alternativa
        - Documentar racional
```

---

## Guardrails de auto-fix

### Guardrail 1: Não renomear sem racional

Toda renomeação MUST ser documentada com:

- nome anterior
- nome novo
- tipo de transformação
- risco avaliado
- razão técnica

### Guardrail 2: Não quebrar contratos externos

Se rename pode quebrar:

- queries em produção
- APIs externas
- documentação
- linhagem de dados

Então: **NÃO auto-fix**

### Guardrail 3: Não inventar semântica

Se unidade, tipo ou significado é ambíguo:

- NÃO auto-fix
- Sinalizar para revisão
- Sugerir alternativas

### Guardrail 4: Não renomear sem contexto

Se contexto semântico é incerto:

- NÃO auto-fix
- Solicitar confirmação
- Documentar ambiguidade

### Guardrail 5: Validar consistência antes de aplicar

Antes de aplicar auto-fix:

1. Verificar se novo nome é consistente com resto do codebase
2. Verificar se novo nome não cria conflito
3. Verificar se novo nome segue padrão

---

## Saída de auto-fix

Estruturar como:

```json
{
  "auto_fixed": [
    {
      "original_name": "customerId",
      "new_name": "customer_id",
      "transformation": "camelCase_to_snake_case",
      "risk": "LOW",
      "status": "APPLIED"
    }
  ],
  "requires_review": [
    {
      "original_name": "weight",
      "suggested_name": "weight_kg",
      "transformation": "add_unit",
      "risk": "HIGH",
      "reason": "Unidade é ambígua (kg? lb? oz?)",
      "status": "PENDING_REVIEW"
    }
  ],
  "blocked": [
    {
      "original_name": "fk_customer",
      "suggested_name": "customer_id",
      "transformation": "standardize_foreign_key",
      "risk": "HIGH",
      "reason": "Pode quebrar referências externas",
      "status": "BLOCKED"
    }
  ],
  "summary": {
    "total_violations": 10,
    "auto_fixed": 5,
    "requires_review": 3,
    "blocked": 2
  }
}
```

---

## Exemplo de auto-fix

### Input

```sql
CREATE TABLE customers (
    customerId INT,
    Customer_Name VARCHAR(255),
    email_endereço VARCHAR(255),
    weight DECIMAL(10,2),
    created_date_timestamp TIMESTAMP,
    ativo BOOLEAN
);
```

### Detecção

| Nome | Tipo | Risco | Ação |
|------|------|-------|------|
| customerId | camelCase | LOW | Auto-fix |
| Customer_Name | Casing | LOW | Auto-fix |
| email_endereço | Acentos | LOW | Auto-fix |
| weight | Unidade faltante | HIGH | Revisão |
| created_date_timestamp | Tipo no nome | LOW | Auto-fix |
| ativo | Booleano sem prefixo | MEDIUM | Revisão |

### Auto-fix aplicado

```sql
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(255),
    email_endereco VARCHAR(255),
    weight DECIMAL(10,2),
    created_at TIMESTAMP,
    ativo BOOLEAN
);
```

### Relatório

```
[AUTO-FIXED]
customerId → customer_id
Transformação: camelCase_to_snake_case
Risco: LOW
Status: APPLIED

[AUTO-FIXED]
Customer_Name → customer_name
Transformação: normalize_casing
Risco: LOW
Status: APPLIED

[AUTO-FIXED]
email_endereço → email_endereco
Transformação: remove_accents
Risco: LOW
Status: APPLIED

[AUTO-FIXED]
created_date_timestamp → created_at
Transformação: remove_type_suffix
Risco: LOW
Status: APPLIED

[REQUIRES REVIEW]
weight → weight_kg (ou weight_lb ou weight_oz?)
Transformação: add_unit
Risco: HIGH
Razão: Unidade é ambígua
Status: PENDING_REVIEW

[REQUIRES REVIEW]
ativo → is_active
Transformação: add_boolean_prefix
Risco: MEDIUM
Razão: Requer confirmação de tipo BOOLEAN
Status: PENDING_REVIEW
```

---

## Limites

Esta skill fornece procedimento de auto-fix.

Esta skill não substitui:

- política de naming
- regras específicas
- validação
- detecção
- prompts de enforcement

---

## Relação com demais artefatos

- referencia `../../rules/naming/README.md`
- referencia regras específicas selecionadas pelo roteador de naming
- referencia `../../rules/naming/reference-units.md`
- referencia `../../rules/naming/reference-severity.md`
- referencia `../../governance/composition/semantic-naming-governance.md`
- consome `./semantic-naming-detection.md`
- é acionada por `../../prompts/review/enforce-semantic-naming.md`
