# rule-07-dates

## Tipo do artefato

rule

## Finalidade

Definir padrão obrigatório para nomes de colunas de data e timestamp.

---

## Quando usar

Use esta regra quando precisar:

- nomear colunas de data
- validar conformidade de datas
- revisar nomes de timestamps
- implementar linter de datas

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

**Princípio:** Colunas de data devem ser imediatamente identificáveis pelo nome.

### Aplicação

Colunas de data MUST usar sufixo `_date` ou `_at`.

---

## Padrão

### `<event>_date` para datas

Use `_date` quando a coluna armazena apenas data (YYYY-MM-DD).

**Exemplos:**
```
created_date        (data de criação)
updated_date        (data de atualização)
birth_date          (data de nascimento)
invoice_date        (data da fatura)
order_date          (data do pedido)
start_date          (data de início)
end_date            (data de término)
due_date            (data de vencimento)
```

---

### `<event>_at` para timestamps

Use `_at` quando a coluna armazena data e hora (YYYY-MM-DD HH:MM:SS).

**Exemplos:**
```
created_at          (criado em)
updated_at          (atualizado em)
deleted_at          (deletado em)
published_at        (publicado em)
started_at          (iniciado em)
ended_at            (terminado em)
last_login_at       (último login em)
```

---

## Exemplos de conformidade

### Exemplo 1: Correto (_date)

**Nome:** `created_date`

```sql
CREATE TABLE customers (
    customer_id INT,
    created_date DATE
);
```

**Validação:**
- É data? ✅
- Tem sufixo _date ou _at? ✅ (_date)
- Tipo é DATE? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 2: Correto (_at)

**Nome:** `created_at`

```sql
CREATE TABLE customers (
    customer_id INT,
    created_at TIMESTAMP
);
```

**Validação:**
- É timestamp? ✅
- Tem sufixo _date ou _at? ✅ (_at)
- Tipo é TIMESTAMP? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 3: Incorreto

**Nome:** `created`

```sql
CREATE TABLE customers (
    customer_id INT,
    created TIMESTAMP
);
```

**Validação:**
- É data/timestamp? ✅
- Tem sufixo _date ou _at? ❌
- Ambíguo se é data? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** created_at (ou created_date)

---

### Exemplo 4: Incorreto

**Nome:** `dt_criacao`

```sql
CREATE TABLE customers (
    customer_id INT,
    dt_criacao TIMESTAMP
);
```

**Validação:**
- É data/timestamp? ✅
- Tem sufixo _date ou _at? ❌
- Usa abreviação? ✅ (dt)
- Idioma misto? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** created_at

---

## Severidade

**Severidade:** HIGH

Datas sem sufixo causam:
- Ambiguidade (é data ou string?)
- Dificuldade de leitura
- Erros de interpretação
- Problemas em linhagem de dados

---

## Auto-fix condicional

Adicionar sufixo é permitido APENAS se tipo de dado é confirmado como DATE ou TIMESTAMP.

**Procedimento:**
1. Verificar tipo de dado
2. Se DATE, adicionar _date
3. Se TIMESTAMP, adicionar _at
4. Se outro tipo, sinalizar para revisão

---

## Procedimento de validação

### Passo 1: Identificar colunas de data

Listar todas as colunas com tipo DATE ou TIMESTAMP:

```sql
SELECT column_name, data_type
FROM information_schema.columns
WHERE data_type IN ('date', 'timestamp', 'datetime')
```

---

### Passo 2: Para cada coluna, verificar sufixo

```
Colunas de data:
- created: tem sufixo? ❌
- updated: tem sufixo? ❌
- created_date: tem sufixo? ✅
- created_at: tem sufixo? ✅
```

---

### Passo 3: Se falta sufixo, sinalizar

```
Violações encontradas:
1. created (deveria ser created_date ou created_at)
2. updated (deveria ser updated_date ou updated_at)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE orders (
    order_id INT,
    created TIMESTAMP,
    updated TIMESTAMP,
    shipped DATE,
    delivered DATE
);
```

### Detecção

```
Datas sem sufixo:
1. created (deveria ser created_at)
2. updated (deveria ser updated_at)
3. shipped (deveria ser shipped_date)
4. delivered (deveria ser delivered_date)

Severidade: HIGH
Ação: REQUER REVISÃO
```

---

## Exemplo de auto-fix

### Input

```
created (TIMESTAMP)
updated (TIMESTAMP)
shipped (DATE)
delivered (DATE)
```

### Auto-fix (condicional)

```
created → created_at (se tipo é TIMESTAMP)
updated → updated_at (se tipo é TIMESTAMP)
shipped → shipped_date (se tipo é DATE)
delivered → delivered_date (se tipo é DATE)
```

---

## Distinção: _date vs. _at

| Sufixo | Tipo | Formato | Exemplo |
|--------|------|---------|---------|
| _date | DATE | YYYY-MM-DD | birth_date |
| _at | TIMESTAMP | YYYY-MM-DD HH:MM:SS | created_at |

**Importante:** Escolher sufixo baseado no tipo de dado, não na preferência.

---

## Limites

Esta regra governa nomes de datas.

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
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 6)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformação 8)
