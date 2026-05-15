# rule-06-booleans

## Tipo do artefato

rule

## Finalidade

Definir padrão obrigatório para nomes de colunas booleanas.

---

## Quando usar

Use esta regra quando precisar:

- nomear colunas booleanas
- validar conformidade de booleanos
- revisar nomes de flags e status
- implementar linter de booleanos

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

**Princípio:** Colunas booleanas devem ser imediatamente identificáveis pelo nome.

### Aplicação

Colunas booleanas MUST usar prefixo `is_` ou `has_`.

---

## Padrão

### `is_<property>` para estado

Use `is_` quando a coluna representa um estado ou condição.

**Exemplos:**
```
is_active           (está ativo?)
is_deleted          (está deletado?)
is_primary          (é primário?)
is_verified         (está verificado?)
is_published        (está publicado?)
is_archived         (está arquivado?)
is_locked           (está bloqueado?)
is_enabled          (está habilitado?)
```

---

### `has_<property>` para posse

Use `has_` quando a coluna representa posse ou existência.

**Exemplos:**
```
has_address         (tem endereço?)
has_phone           (tem telefone?)
has_email           (tem email?)
has_discount        (tem desconto?)
has_attachment      (tem anexo?)
has_children        (tem filhos?)
has_permission      (tem permissão?)
```

---

## Exemplos de conformidade

### Exemplo 1: Correto (is_)

**Nome:** `is_active`

```sql
CREATE TABLE customers (
    customer_id INT,
    is_active BOOLEAN
);
```

**Validação:**
- É booleano? ✅
- Tem prefixo is_ ou has_? ✅ (is_)
- Comunica estado? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 2: Correto (has_)

**Nome:** `has_address`

```sql
CREATE TABLE customers (
    customer_id INT,
    has_address BOOLEAN
);
```

**Validação:**
- É booleano? ✅
- Tem prefixo is_ ou has_? ✅ (has_)
- Comunica posse? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 3: Incorreto

**Nome:** `active`

```sql
CREATE TABLE customers (
    customer_id INT,
    active BOOLEAN
);
```

**Validação:**
- É booleano? ✅
- Tem prefixo is_ ou has_? ❌
- Ambíguo se é booleano? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** is_active

---

### Exemplo 4: Incorreto

**Nome:** `deleted`

```sql
CREATE TABLE customers (
    customer_id INT,
    deleted BOOLEAN
);
```

**Validação:**
- É booleano? ✅
- Tem prefixo is_ ou has_? ❌
- Ambíguo se é booleano? ✅

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** is_deleted

---

## Severidade

**Severidade:** MEDIUM

Booleanos sem prefixo causam:
- Ambiguidade (é booleano ou string?)
- Dificuldade de leitura
- Erros de interpretação

---

## Auto-fix condicional

Adicionar prefixo é permitido APENAS se tipo de dado é confirmado como BOOLEAN.

**Procedimento:**
1. Verificar tipo de dado
2. Se BOOLEAN, adicionar is_ ou has_
3. Se não BOOLEAN, sinalizar para revisão

---

## Procedimento de validação

### Passo 1: Identificar colunas booleanas

Listar todas as colunas com tipo BOOLEAN:

```sql
SELECT column_name, data_type
FROM information_schema.columns
WHERE data_type = 'boolean'
```

---

### Passo 2: Para cada coluna, verificar prefixo

```
Colunas booleanas:
- active: tem prefixo? ❌
- deleted: tem prefixo? ❌
- is_verified: tem prefixo? ✅
- has_address: tem prefixo? ✅
```

---

### Passo 3: Se falta prefixo, sinalizar

```
Violações encontradas:
1. active (deveria ser is_active)
2. deleted (deveria ser is_deleted)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE customers (
    customer_id INT,
    active BOOLEAN,
    deleted BOOLEAN,
    verified BOOLEAN,
    address BOOLEAN
);
```

### Detecção

```
Booleanos sem prefixo:
1. active (deveria ser is_active)
2. deleted (deveria ser is_deleted)
3. verified (deveria ser is_verified)
4. address (deveria ser has_address)

Severidade: MEDIUM
Ação: REQUER REVISÃO
```

---

## Exemplo de auto-fix

### Input

```
active
deleted
verified
address
```

### Auto-fix (condicional)

```
active → is_active (se tipo é BOOLEAN)
deleted → is_deleted (se tipo é BOOLEAN)
verified → is_verified (se tipo é BOOLEAN)
address → has_address (se tipo é BOOLEAN)
```

---

## Limites

Esta regra governa nomes de booleanos.

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
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 5)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformação 7)
