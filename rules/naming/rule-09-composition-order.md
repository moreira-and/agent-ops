# rule-09-composition-order

## Tipo do artefato

rule

## Finalidade

Definir ordem obrigatória de componentes em nomes compostos.

---

## Quando usar

Use esta regra quando precisar:

- nomear colunas compostas
- validar ordem de componentes
- revisar nomes multi-nível
- implementar linter de ordem

---

## Quando não usar

Não use esta regra como fonte primária para:

- padrão fundamental
- formato de nomes
- consistência semântica
- unidades
- abreviações

Consulte, respectivamente:

- `./_core-pattern.md`
- `./rule-01-format.md`
- `./rule-02-consistency.md`
- `./rule-03-units.md`
- `./rule-04-abbreviations.md`

---

## Dependências relacionadas

- `./_core-pattern.md`

---

## Regra

**Princípio:** Nomes compostos devem ser ordenados por hierarquia semântica, do mais geral para o mais específico.

### Aplicação

Componentes MUST ser ordenados: `entity → detail → property → unit`

---

## Padrão

### Ordem obrigatória

```
entity_detail_property_unit
```

**Interpretação:**
1. **entity** - conceito principal (mais geral)
2. **detail** - refinamento ou contexto
3. **property** - atributo ou medida
4. **unit** - unidade (mais específico)

---

## Exemplos de ordem correta

### Exemplo 1: Simples

```
customer_name

Ordem:
- entity: customer (geral)
- property: name (específico)
```

---

### Exemplo 2: Com detail

```
customer_billing_address

Ordem:
- entity: customer (geral)
- detail: billing (contexto)
- property: address (específico)
```

---

### Exemplo 3: Com unidade

```
product_net_weight_kg

Ordem:
- entity: product (geral)
- detail: net (contexto)
- property: weight (medida)
- unit: kg (específico)
```

---

### Exemplo 4: Complexo

```
order_line_item_quantity

Ordem:
- entity: order (geral)
- detail: line_item (contexto)
- property: quantity (específico)
```

---

## Exemplos de ordem incorreta

### Exemplo 1: Ordem invertida

**Incorreto:**
```
address_customer_billing

Ordem:
- address (específico)
- customer (geral)
- billing (contexto)

Problema: Ordem invertida (específico → geral)
```

**Correto:**
```
customer_billing_address

Ordem:
- customer (geral)
- billing (contexto)
- address (específico)
```

---

### Exemplo 2: Ordem invertida

**Incorreto:**
```
item_line_order_quantity

Ordem:
- item (específico)
- line (contexto)
- order (geral)
- quantity (específico)

Problema: Ordem confusa
```

**Correto:**
```
order_line_item_quantity

Ordem:
- order (geral)
- line_item (contexto)
- quantity (específico)
```

---

### Exemplo 3: Ordem invertida

**Incorreto:**
```
price_variant_product_brl

Ordem:
- price (específico)
- variant (contexto)
- product (geral)
- brl (unidade)

Problema: Ordem invertida
```

**Correto:**
```
product_variant_price_brl

Ordem:
- product (geral)
- variant (contexto)
- price (medida)
- brl (unidade)
```

---

## Severidade

**Severidade:** MEDIUM

Ordem incorreta causa:
- Dificuldade de leitura
- Confusão semântica
- Problemas em sorting/grouping
- Erros de interpretação

---

## Auto-fix permitido

Reordenar componentes é permitido se ordem é clara.

**Procedimento:**
1. Decompor nome em componentes
2. Classificar cada componente (entity, detail, property, unit)
3. Reordenar: entity → detail → property → unit
4. Reconstruir nome

---

## Procedimento de validação

### Passo 1: Decompor nome

```
Nome: address_customer_billing

Componentes:
- address
- customer
- billing
```

---

### Passo 2: Classificar cada componente

```
Classificação:
- address: property (atributo)
- customer: entity (conceito principal)
- billing: detail (contexto)
```

---

### Passo 3: Verificar ordem

```
Ordem esperada: entity → detail → property → unit
Ordem atual: property → entity → detail

Resultado: ❌ ORDEM INCORRETA
```

---

### Passo 4: Reordenar

```
Ordem correta: entity → detail → property
Novo nome: customer_billing_address
```

---

## Exemplo de detecção

### Input

```
address_customer_billing
item_line_order_quantity
price_variant_product_brl
weight_product_net_kg
```

### Detecção

```
Ordem incorreta:
1. address_customer_billing
   Atual: property → entity → detail
   Correto: customer_billing_address (entity → detail → property)

2. item_line_order_quantity
   Atual: property → detail → entity → property
   Correto: order_line_item_quantity (entity → detail → property)

3. price_variant_product_brl
   Atual: property → detail → entity → unit
   Correto: product_variant_price_brl (entity → detail → property → unit)

4. weight_product_net_kg
   Atual: property → entity → detail → unit
   Correto: product_net_weight_kg (entity → detail → property → unit)

Severidade: MEDIUM
Ação: REQUER REVISÃO
```

---

## Exemplo de auto-fix

### Input

```
address_customer_billing
item_line_order_quantity
price_variant_product_brl
```

### Auto-fix

```
address_customer_billing → customer_billing_address
item_line_order_quantity → order_line_item_quantity
price_variant_product_brl → product_variant_price_brl
```

---

## Limites

Esta regra governa ordem de componentes.

Esta regra não governa:

- padrão fundamental
- formato de nomes
- consistência semântica
- unidades
- abreviações
- tipos

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 9)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformação 9)
