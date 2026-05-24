# Semantic naming examples

## Tipo do artefato

human documentation / examples

## Finalidade

Registrar exemplos completos de naming semantico fora do contexto injetavel padrao.

Este arquivo ajuda humanos a entender a aplicacao das regras. Ele nao define norma primaria, severidade, unidade valida ou procedimento de auto-fix.

---

## Fontes normativas

- Regras: `../../rules/naming/README.md`
- Severidade: `../../rules/naming/reference-severity.md`
- Unidades: `../../rules/naming/reference-units.md`
- Validacao: `../../skills/review/semantic-naming-validation.md`
- Deteccao: `../../skills/review/semantic-naming-detection.md`
- Auto-fix: `../../skills/review/semantic-naming-autofix.md`

---

## Exemplo 1: schema conforme

Entrada:

```sql
CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    order_total_amount_brl DECIMAL(10,2),
    order_created_at TIMESTAMP,
    is_active BOOLEAN
);
```

Resultado esperado:

```txt
status: PASS
violations_total: 0
recommendation: APPROVE
```

Racional:

- `customer_id` usa o padrao de chave estrangeira.
- `order_total_amount_brl` declara moeda.
- `order_created_at` usa sufixo de timestamp.
- `is_active` usa prefixo booleano.

---

## Exemplo 2: schema com violacoes

Entrada:

```sql
CREATE TABLE orders (
    id_order INT,
    fk_customer INT,
    vlr_total DECIMAL(10,2),
    data_criacao TIMESTAMP,
    ativo BOOLEAN
);
```

Resultado esperado resumido:

| Nome | Regra | Severidade esperada | Decisao esperada | Racional |
|---|---|---|---|---|
| `id_order` | `rule-01-format.md` ou `rule-09-composition-order.md` | conforme `reference-severity.md` | `REQUIRES_REVIEW` | ordem invertida |
| `fk_customer` | `rule-08-foreign-keys.md` | `CRITICAL` | `BLOCKED` | prefixo tecnico e risco de contrato |
| `vlr_total` | `rule-03-units.md`, `rule-04-abbreviations.md` | conforme `reference-severity.md` | `REQUIRES_REVIEW` | abreviacao e moeda ambigua |
| `data_criacao` | `rule-04-abbreviations.md`, `rule-07-dates.md` | conforme `reference-severity.md` | `REQUIRES_REVIEW` | idioma misto e padrao de data |
| `ativo` | `rule-06-booleans.md` | conforme `reference-severity.md` | `REQUIRES_REVIEW` | tipo booleano precisa evidencia |

Resultado esperado:

```txt
status: FAIL
recommendation: BLOCK
reason: fk_customer viola rule-08-foreign-keys.md e e bloqueante conforme reference-severity.md
```

---

## Exemplo 3: unidade ambigua bloqueia auto-fix

Entrada:

```sql
CREATE TABLE products (
    product_id INT,
    weight DECIMAL(10,2)
);
```

Resultado esperado:

```txt
name: weight
rule: rule-03-units.md
decision: REQUIRES_REVIEW
auto_fix: BLOCKED_BY_DEFAULT
suggested_options: weight_kg | weight_lb | weight_oz
reason: unidade nao foi informada no input
```

Racional:

- `weight_kg` nao pode ser aplicado automaticamente sem evidencia.
- A lista de unidades vem de `../../rules/naming/reference-units.md`.

---

## Exemplo 4: auto-fix lexical seguro

Entrada:

```sql
CREATE TABLE customers (
    customerId INT,
    Customer_Name VARCHAR(255),
    customer__email VARCHAR(255)
);
```

Resultado esperado:

```txt
customerId -> customer_id
Customer_Name -> customer_name
customer__email -> customer_email
```

Racional:

- Conversao de casing e separador e deterministica.
- Nenhuma unidade, entidade ambigua ou contrato externo foi inferido.
- O agente ainda deve registrar o diff e o racional.

---

## Exemplo 5: rename bloqueado por contrato

Entrada:

```sql
CREATE TABLE orders (
    order_id INT,
    fk_customer INT,
    FOREIGN KEY (fk_customer) REFERENCES customers(customer_id)
);
```

Resultado esperado:

```txt
name: fk_customer
suggested_name: customer_id
rule: rule-08-foreign-keys.md
severity: CRITICAL
decision: BLOCKED
reason: rename de chave estrangeira pode quebrar contrato, query, linagem ou migracao
```

---

## Limites

Este arquivo e explicativo. Em execucao agentica, carregue regras, skills e prompts operacionais; carregue este exemplo apenas quando o usuario pedir contexto humano ou exemplo completo.
