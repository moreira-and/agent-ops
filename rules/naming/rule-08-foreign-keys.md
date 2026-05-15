# rule-08-foreign-keys

## Tipo do artefato

rule

## Finalidade

Definir padrão obrigatório para nomes de chaves estrangeiras.

---

## Quando usar

Use esta regra quando precisar:

- nomear colunas de chave estrangeira
- validar conformidade de chaves
- revisar nomes de referências
- implementar linter de chaves

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

**Princípio:** Chaves estrangeiras devem usar padrão semântico, não técnico.

### Aplicação

Colunas de chave estrangeira MUST usar padrão `<referenced_entity>_id`.

---

## Padrão

### `<referenced_entity>_id`

Use o nome da entidade referenciada seguido de `_id`.

**Exemplos:**
```
customer_id         (referencia tabela customers)
product_id          (referencia tabela products)
order_id            (referencia tabela orders)
invoice_id          (referencia tabela invoices)
employee_id         (referencia tabela employees)
department_id       (referencia tabela departments)
```

---

## Exemplos de conformidade

### Exemplo 1: Correto

**Nome:** `customer_id`

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

**Validação:**
- É chave estrangeira? ✅
- Segue padrão <entity>_id? ✅
- Referencia entidade correta? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 2: Incorreto (prefixo técnico)

**Nome:** `fk_customer`

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    fk_customer INT,
    FOREIGN KEY (fk_customer) REFERENCES customers(customer_id)
);
```

**Validação:**
- É chave estrangeira? ✅
- Segue padrão <entity>_id? ❌ (usa prefixo fk_)
- Usa prefixo técnico? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** customer_id

---

### Exemplo 3: Incorreto (ordem invertida)

**Nome:** `id_customer`

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    id_customer INT,
    FOREIGN KEY (id_customer) REFERENCES customers(customer_id)
);
```

**Validação:**
- É chave estrangeira? ✅
- Segue padrão <entity>_id? ❌ (ordem invertida)
- Ordem é entity_id? ❌

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** customer_id

---

### Exemplo 4: Incorreto (abreviação)

**Nome:** `cust_id`

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    cust_id INT,
    FOREIGN KEY (cust_id) REFERENCES customers(customer_id)
);
```

**Validação:**
- É chave estrangeira? ✅
- Segue padrão <entity>_id? ❌ (abreviação)
- Usa abreviação? ✅ (cust)

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** customer_id

---

## Severidade

**Severidade:** HIGH

Chaves estrangeiras com padrão técnico causam:
- Inconsistência semântica
- Dificuldade de linhagem
- Erros de join
- Confusão em análises

---

## Auto-fix bloqueado

Renomear chaves estrangeiras é BLOQUEADO.

**Razão:** Pode quebrar referências externas, queries em produção, documentação.

**Procedimento:**
1. Detectar violação
2. Sinalizar para revisão humana
3. Sugerir alternativa
4. Solicitar confirmação

---

## Procedimento de validação

### Passo 1: Identificar chaves estrangeiras

Listar todas as colunas que são chaves estrangeiras:

```sql
SELECT column_name, referenced_table_name
FROM information_schema.key_column_usage
WHERE referenced_table_name IS NOT NULL
```

---

### Passo 2: Para cada chave, verificar padrão

```
Chaves estrangeiras:
- customer_id: segue padrão? ✅
- fk_customer: segue padrão? ❌
- id_customer: segue padrão? ❌
- cust_id: segue padrão? ❌
```

---

### Passo 3: Se não segue padrão, sinalizar

```
Violações encontradas:
1. fk_customer (deveria ser customer_id)
2. id_customer (deveria ser customer_id)
3. cust_id (deveria ser customer_id)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    fk_customer INT,
    id_product INT,
    cust_invoice INT,
    FOREIGN KEY (fk_customer) REFERENCES customers(customer_id),
    FOREIGN KEY (id_product) REFERENCES products(product_id),
    FOREIGN KEY (cust_invoice) REFERENCES invoices(invoice_id)
);
```

### Detecção

```
Chaves estrangeiras com padrão incorreto:
1. fk_customer (deveria ser customer_id)
2. id_product (deveria ser product_id)
3. cust_invoice (deveria ser invoice_id)

Severidade: HIGH
Ação: BLOQUEIA MERGE
Razão: Pode quebrar referências externas
```

---

## Padrões proibidos

| Proibido | Correto | Razão |
|----------|---------|-------|
| fk_customer | customer_id | Prefixo técnico |
| id_customer | customer_id | Ordem invertida |
| cust_id | customer_id | Abreviação |
| customer_fk | customer_id | Sufixo técnico |
| customer_key | customer_id | Sufixo técnico |
| customer_ref | customer_id | Abreviação |

---

## Limites

Esta regra governa nomes de chaves estrangeiras.

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
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 7)
- é bloqueada por `../../skills/review/semantic-naming-autofix.md` (não auto-fix)
