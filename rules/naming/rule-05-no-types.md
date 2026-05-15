# rule-05-no-types

## Tipo do artefato

rule

## Finalidade

Definir proibição de codificar tipos de dados em nomes semânticos.

---

## Quando usar

Use esta regra quando precisar:

- validar se um nome contém tipo de dado
- identificar violações de tipo em nome
- revisar conformidade de nomenclatura
- implementar linter de tipos

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

**Princípio:** Tipos de dados pertencem ao schema, não ao nome semântico.

### Aplicação

Nomes MUST NOT conter sufixos que indicam tipo de dado.

---

## Tipos proibidos em nomes

| Proibido | Correto | Razão |
|----------|---------|-------|
| customer_id_int | customer_id | Tipo pertence ao schema |
| amount_float | amount | Tipo pertence ao schema |
| name_string | name | Tipo pertence ao schema |
| is_active_boolean | is_active | Tipo pertence ao schema |
| created_date_timestamp | created_at | Tipo pertence ao schema |
| count_integer | count | Tipo pertence ao schema |
| price_decimal | price | Tipo pertence ao schema |
| status_varchar | status | Tipo pertence ao schema |
| weight_numeric | weight | Tipo pertence ao schema |
| flag_bit | flag | Tipo pertence ao schema |

---

## Exemplos de conformidade

### Exemplo 1: Correto

**Nome:** `customer_id`

```sql
CREATE TABLE customers (
    customer_id INT,  -- Tipo definido no schema
    customer_name VARCHAR(255),
    is_active BOOLEAN
);
```

**Validação:**
- Nome contém tipo? ❌
- Tipo está no schema? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 2: Incorreto

**Nome:** `customer_id_int`

```sql
CREATE TABLE customers (
    customer_id_int INT,  -- Tipo codificado no nome
    customer_name_string VARCHAR(255),
    is_active_boolean BOOLEAN
);
```

**Validação:**
- Nome contém tipo? ✅ (_int, _string, _boolean)
- Tipo está no schema? ✅

**Resultado:** ❌ VIOLAÇÃO (duplicação)

**Sugestão:** customer_id, customer_name, is_active

---

### Exemplo 3: Correto

**Nome:** `amount_brl`

```sql
CREATE TABLE invoices (
    amount_brl DECIMAL(10,2),  -- Unidade no nome, tipo no schema
    created_at TIMESTAMP
);
```

**Validação:**
- Nome contém tipo? ❌
- Nome contém unidade? ✅ (brl é unidade, não tipo)
- Tipo está no schema? ✅

**Resultado:** ✅ VÁLIDO

---

## Severidade

**Severidade:** MEDIUM

Codificar tipos em nomes causa:
- Duplicação de informação
- Confusão semântica
- Dificuldade de manutenção
- Violação de separação de responsabilidades

---

## Auto-fix permitido

Transformações automáticas permitidas:

- customer_id_int → customer_id
- amount_float → amount
- name_string → name
- is_active_boolean → is_active
- created_date_timestamp → created_at
- count_integer → count

---

## Procedimento de validação

### Passo 1: Extrair sufixos de tipo

Listar sufixos comuns de tipo:

```
Sufixos de tipo:
- _int, _integer
- _float, _double, _decimal, _numeric
- _string, _varchar, _text
- _boolean, _bit, _flag
- _timestamp, _datetime, _date, _time
- _blob, _binary
```

---

### Passo 2: Para cada nome, verificar se contém sufixo

```
Nomes:
- customer_id: contém sufixo? ❌
- customer_id_int: contém sufixo? ✅ (_int)
- amount_float: contém sufixo? ✅ (_float)
- is_active_boolean: contém sufixo? ✅ (_boolean)
```

---

### Passo 3: Se houver sufixo, sinalizar

```
Violações encontradas:
1. customer_id_int (remover _int)
2. amount_float (remover _float)
3. is_active_boolean (remover _boolean)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE products (
    product_id_int INT,
    product_name_string VARCHAR(255),
    price_decimal DECIMAL(10,2),
    is_available_boolean BOOLEAN,
    created_at_timestamp TIMESTAMP
);
```

### Detecção

```
Tipos codificados em nomes:
1. product_id_int (sufixo _int)
2. product_name_string (sufixo _string)
3. price_decimal (sufixo _decimal)
4. is_available_boolean (sufixo _boolean)
5. created_at_timestamp (sufixo _timestamp)

Severidade: MEDIUM
Ação: REQUER REVISÃO
```

---

## Exemplo de auto-fix

### Input

```
customer_id_int
amount_float
name_string
is_active_boolean
created_date_timestamp
```

### Auto-fix

```
customer_id_int → customer_id
amount_float → amount
name_string → name
is_active_boolean → is_active
created_date_timestamp → created_at
```

---

## Distinção: Tipo vs. Unidade

**Importante:** Não confundir tipo com unidade.

### Tipo (PROIBIDO em nome)
```
_int, _float, _string, _boolean, _timestamp
```

### Unidade (OBRIGATÓRIO em nome)
```
_kg, _brl, _celsius, _m, _percent
```

### Exemplo

```
weight_kg_float     ❌ VIOLAÇÃO
                    - _float é tipo (proibido)
                    - _kg é unidade (obrigatório)

weight_kg           ✅ VÁLIDO
                    - _kg é unidade (obrigatório)
                    - Tipo (DECIMAL) está no schema
```

---

## Limites

Esta regra governa tipos em nomes.

Esta regra não governa:

- padrão fundamental
- formato de nomes
- consistência semântica
- unidades
- abreviações
- casos especiais

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 4)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformação 6)
