# rule-01-format

## Tipo do artefato

rule

## Finalidade

Definir restrições obrigatórias de formato para nomes semânticos.

---

## Quando usar

Use esta regra quando precisar:

- validar se um nome segue formato correto
- corrigir violações de casing, acentos, espaços
- revisar conformidade de formato
- implementar linter de formato

---

## Quando não usar

Não use esta regra como fonte primária para:

- padrão fundamental
- consistência semântica
- unidades
- abreviações

Consulte, respectivamente:

- `./_core-pattern.md`
- `./rule-02-consistency.md`
- `./rule-03-units.md`
- `./rule-04-abbreviations.md`

---

## Dependências relacionadas

- `./_core-pattern.md`

---

## Regra

**Padrão:** `entity_detail_property_unit`

### Restrições obrigatórias

#### 1. MUST usar snake_case

Separar componentes com underscore, sem espaços.

**Correto:**
```
customer_id
customer_name
product_net_weight_kg
order_shipping_address
```

**Incorreto:**
```
customerId              # camelCase
customer-id             # hífen
customer id             # espaço
customer.id             # ponto
```

---

#### 2. MUST usar lowercase

Todos os caracteres devem ser minúsculos.

**Correto:**
```
customer_id
product_name
invoice_total_amount_brl
```

**Incorreto:**
```
Customer_ID             # maiúsculas
CUSTOMER_ID             # maiúsculas
Customer_name           # maiúscula inicial
```

---

#### 3. MUST NOT conter acentos

Remover acentos de caracteres acentuados.

**Correto:**
```
cliente_endereco        # sem acentos
produto_descricao       # sem acentos
data_criacao            # sem acentos
```

**Incorreto:**
```
cliente_endereço        # com acento
produto_descrição       # com acento
data_criação            # com acento
```

---

#### 4. MUST NOT conter espaços

Usar underscore em vez de espaços.

**Correto:**
```
customer_billing_address
product_unit_price_brl
order_line_item_quantity
```

**Incorreto:**
```
customer billing address
product unit price brl
order line item quantity
```

---

#### 5. MUST NOT conter caracteres especiais

Apenas underscore é permitido como separador.

**Correto:**
```
customer_id
product_name
invoice_total_amount_brl
```

**Incorreto:**
```
customer@id             # @
product#name            # #
invoice$total           # $
customer&id             # &
```

---

#### 6. MUST ser determinístico

Mesmo conceito semântico deve sempre usar exatamente o mesmo nome.

**Correto:**
```
Tabela A: customer_id
Tabela B: customer_id
Tabela C: customer_id
```

**Incorreto:**
```
Tabela A: customer_id
Tabela B: customerId
Tabela C: customer_ID
```

---

## Severidade

**Severidade:** HIGH

Violações de formato são facilmente detectáveis e corrigíveis automaticamente.

---

## Auto-fix permitido

Transformações automáticas permitidas:

- camelCase → snake_case
- UPPERCASE → lowercase
- Acentos → sem acentos
- Espaços → underscores
- Caracteres especiais → underscores

---

## Exemplos de validação

### Exemplo 1: Violação de casing

**Nome:** `CustomerID`

**Validação:**
- snake_case? ❌ (camelCase)
- lowercase? ❌ (maiúsculas)
- sem acentos? ✅
- sem espaços? ✅
- sem caracteres especiais? ✅
- determinístico? ❌ (variação de casing)

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** `customer_id`

**Auto-fix:** SIM

---

### Exemplo 2: Violação de acentos

**Nome:** `cliente_endereço`

**Validação:**
- snake_case? ✅
- lowercase? ✅
- sem acentos? ❌ (ç)
- sem espaços? ✅
- sem caracteres especiais? ✅
- determinístico? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** `cliente_endereco`

**Auto-fix:** SIM

---

### Exemplo 3: Válido

**Nome:** `customer_billing_address`

**Validação:**
- snake_case? ✅
- lowercase? ✅
- sem acentos? ✅
- sem espaços? ✅
- sem caracteres especiais? ✅
- determinístico? ✅

**Resultado:** ✅ VÁLIDO

---

## Limites

Esta regra governa formato.

Esta regra não governa:

- padrão fundamental
- consistência semântica
- unidades
- abreviações
- tipos
- casos especiais (booleanos, datas, chaves)

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 1)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformações 1-3)
