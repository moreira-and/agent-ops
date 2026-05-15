# rule-02-consistency

## Tipo do artefato

rule

## Finalidade

Definir obrigatoriedade de consistência semântica em nomes.

---

## Quando usar

Use esta regra quando precisar:

- validar consistência entre múltiplas tabelas
- identificar variações de mesmo conceito
- revisar linhagem de dados
- auditar conformidade semântica

---

## Quando não usar

Não use esta regra como fonte primária para:

- padrão fundamental
- formato de nomes
- unidades
- abreviações

Consulte, respectivamente:

- `./_core-pattern.md`
- `./rule-01-format.md`
- `./rule-03-units.md`
- `./rule-04-abbreviations.md`

---

## Dependências relacionadas

- `./_core-pattern.md`

---

## Regra

**Princípio:** Mesmo conceito semântico = sempre mesmo nome.

### Aplicação

Se múltiplas tabelas, views ou datasets representam o mesmo conceito, usar exatamente o mesmo nome de coluna.

---

## Exemplos de consistência

### Exemplo 1: Correto

**Conceito:** customer_id (identificador de cliente)

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT FOREIGN KEY
);

CREATE TABLE invoices (
    invoice_id INT PRIMARY KEY,
    customer_id INT FOREIGN KEY
);
```

**Validação:**
- customers.customer_id ✅
- orders.customer_id ✅
- invoices.customer_id ✅

**Resultado:** ✅ CONSISTENTE

---

### Exemplo 2: Incorreto

**Conceito:** customer_id (identificador de cliente)

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    id_customer INT FOREIGN KEY
);

CREATE TABLE invoices (
    invoice_id INT PRIMARY KEY,
    fk_customer INT FOREIGN KEY
);
```

**Validação:**
- customers.customer_id ✅
- orders.id_customer ❌ (variação)
- invoices.fk_customer ❌ (variação)

**Resultado:** ❌ INCONSISTENTE

**Violações bloqueadas:**
- customer_id vs. id_customer
- customer_id vs. fk_customer
- customer_id vs. cod_customer
- customer_id vs. customer_code
- customer_id vs. cust_id

---

## Severidade

**Severidade:** CRITICAL

Inconsistência semântica quebra:
- Discoverabilidade
- Linhagem de dados
- Raciocínio automatizado
- Manutenção

---

## Auto-fix bloqueado

Renomeações por inconsistência semântica MUST ser revisadas manualmente.

**Razão:** Pode quebrar referências externas, queries em produção, documentação.

---

## Procedimento de validação

### Passo 1: Identificar conceitos semânticos

Listar todos os conceitos únicos representados:

```
Conceitos:
- customer (cliente)
- product (produto)
- order (pedido)
- invoice (fatura)
```

---

### Passo 2: Para cada conceito, coletar nomes

```
Conceito: customer
Nomes encontrados:
- customers.customer_id
- orders.customer_id
- invoices.customer_id
- shipments.customer_id
```

---

### Passo 3: Verificar se todos os nomes são idênticos

```
Validação:
- customers.customer_id ✅
- orders.customer_id ✅
- invoices.customer_id ✅
- shipments.customer_id ✅

Resultado: ✅ CONSISTENTE
```

---

### Passo 4: Se houver variações, sinalizar

```
Conceito: customer
Nomes encontrados:
- customers.customer_id ✅
- orders.id_customer ❌
- invoices.fk_customer ❌
- shipments.cod_customer ❌

Resultado: ❌ INCONSISTENTE

Violações:
- orders.id_customer (deveria ser customer_id)
- invoices.fk_customer (deveria ser customer_id)
- shipments.cod_customer (deveria ser customer_id)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(255)
);

CREATE TABLE orders (
    order_id INT,
    id_customer INT,
    order_date DATE
);

CREATE TABLE invoices (
    invoice_id INT,
    fk_customer INT,
    invoice_date DATE
);
```

### Detecção

```
Conceito: customer
Nomes encontrados:
- customers.customer_id
- orders.id_customer
- invoices.fk_customer

Inconsistências detectadas:
1. orders.id_customer (deveria ser customer_id)
2. invoices.fk_customer (deveria ser customer_id)

Severidade: CRITICAL
Ação: BLOQUEIA MERGE
```

---

## Limites

Esta regra governa consistência semântica.

Esta regra não governa:

- padrão fundamental
- formato de nomes
- unidades
- abreviações
- tipos
- casos especiais

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 8)
- é bloqueada por `../../skills/review/semantic-naming-autofix.md` (não auto-fix)
