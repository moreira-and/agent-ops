# rule-10-avoid-generic

## Tipo do artefato

rule

## Finalidade

Definir proibição de nomes genéricos ou vagos.

---

## Quando usar

Use esta regra quando precisar:

- validar especificidade de nomes
- identificar nomes vagos
- revisar clareza de nomenclatura
- implementar linter de genericidade

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

**Princípio:** Nomes devem comunicar significado específico, não ser genéricos ou vagos.

### Aplicação

Nomes MUST NOT ser genéricos ou ambíguos.

---

## Nomes genéricos proibidos

| Proibido | Razão | Correto |
|----------|-------|---------|
| data | Muito vago (qual dado?) | customer_data → customer_name, customer_email |
| value | Muito vago (qual valor?) | amount_brl, quantity, weight_kg |
| temp | Muito vago (temperatura? temporário?) | temperature_celsius ou temporary_flag |
| var | Muito vago (qual variável?) | <specific_concept> |
| result | Muito vago (qual resultado?) | <specific_outcome> |
| output | Muito vago (qual saída?) | <specific_artifact> |
| x, y, z | Muito vago (qual dimensão?) | <specific_concept> |
| item | Muito vago (qual item?) | order_line_item ou product_item |
| thing | Muito vago (qual coisa?) | <specific_concept> |
| stuff | Muito vago (qual coisa?) | <specific_concept> |
| info | Muito vago (qual informação?) | <specific_information> |
| obj | Muito vago (qual objeto?) | <specific_object> |
| attr | Muito vago (qual atributo?) | <specific_attribute> |
| prop | Muito vago (qual propriedade?) | <specific_property> |
| field | Muito vago (qual campo?) | <specific_field> |
| col | Muito vago (qual coluna?) | <specific_column> |

---

## Exemplos de genericidade

### Exemplo 1: Genérico

**Nome:** `data`

```sql
CREATE TABLE customers (
    customer_id INT,
    data VARCHAR(255)
);
```

**Validação:**
- É específico? ❌ (muito vago)
- Comunica significado? ❌
- Qual dado? ❌ (nome, email, phone?)

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** customer_name, customer_email, customer_phone

---

### Exemplo 2: Genérico

**Nome:** `value`

```sql
CREATE TABLE products (
    product_id INT,
    value DECIMAL(10,2)
);
```

**Validação:**
- É específico? ❌ (muito vago)
- Comunica significado? ❌
- Qual valor? ❌ (preço? peso? quantidade?)

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** price_brl, weight_kg, quantity

---

### Exemplo 3: Genérico

**Nome:** `temp`

```sql
CREATE TABLE sensors (
    sensor_id INT,
    temp DECIMAL(10,2)
);
```

**Validação:**
- É específico? ❌ (ambíguo)
- Comunica significado? ❌
- Temperatura ou temporário? ❌

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** temperature_celsius ou temporary_flag

---

### Exemplo 4: Específico

**Nome:** `customer_name`

```sql
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(255)
);
```

**Validação:**
- É específico? ✅
- Comunica significado? ✅
- Qual dado? ✅ (nome do cliente)

**Resultado:** ✅ VÁLIDO

---

## Severidade

**Severidade:** LOW

Nomes genéricos causam:
- Dificuldade de compreensão
- Ambiguidade semântica
- Erros de interpretação
- Confusão em análises

---

## Auto-fix bloqueado

Renomear nomes genéricos é BLOQUEADO.

**Razão:** Requer contexto de negócio para determinar nome específico.

**Procedimento:**
1. Detectar nome genérico
2. Sinalizar para revisão humana
3. Sugerir alternativas baseadas em contexto
4. Solicitar confirmação

---

## Procedimento de validação

### Passo 1: Listar nomes genéricos

```
Nomes genéricos:
- data
- value
- temp
- var
- result
- output
- x, y, z
- item
- thing
- stuff
- info
- obj
- attr
- prop
- field
- col
```

---

### Passo 2: Para cada nome, verificar se é genérico

```
Nomes encontrados:
- customer_name: é genérico? ❌
- data: é genérico? ✅
- value: é genérico? ✅
- temperature_celsius: é genérico? ❌
```

---

### Passo 3: Se é genérico, sinalizar

```
Violações encontradas:
1. data (qual dado? nome? email? phone?)
2. value (qual valor? preço? peso? quantidade?)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE customers (
    customer_id INT,
    data VARCHAR(255),
    value DECIMAL(10,2),
    temp DECIMAL(10,2),
    info TEXT
);
```

### Detecção

```
Nomes genéricos:
1. data (qual dado?)
2. value (qual valor?)
3. temp (temperatura? temporário?)
4. info (qual informação?)

Severidade: LOW
Ação: RECOMENDAÇÃO
```

---

## Contexto para renomeação

Para renomear nomes genéricos, considerar:

1. **Domínio de negócio** - Qual é o contexto?
2. **Tipo de dado** - Qual é o tipo?
3. **Unidade** - Qual é a unidade (se mensurável)?
4. **Relacionamento** - Com qual entidade se relaciona?

### Exemplo

**Nome genérico:** `data`

**Contexto:**
- Domínio: e-commerce
- Tabela: customers
- Tipo: VARCHAR
- Relacionamento: customer

**Possíveis renomeações:**
- customer_name
- customer_email
- customer_phone
- customer_address

**Decisão:** Depende do contexto específico

---

## Limites

Esta regra governa genericidade de nomes.

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
- é bloqueada por `../../skills/review/semantic-naming-autofix.md` (não auto-fix)
