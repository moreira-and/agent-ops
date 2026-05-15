# reference-severity

## Tipo do artefato

rule

## Finalidade

Fornecer tabela de referência de severidade de violações de naming.

---

## Quando usar

Use este arquivo quando precisar:

- classificar severidade de violação
- decidir ação (bloqueia, avisa, recomenda)
- priorizar correções
- implementar linter com severidade

---

## Quando não usar

Não use este arquivo como fonte primária para:

- regras específicas
- política de naming
- padrão fundamental

Consulte, respectivamente:

- `./README.md`
- `../../governance/composition/semantic-naming-governance.md`
- `./_core-pattern.md`

---

## Dependências relacionadas

- `./README.md`

---

## Classificação de severidade

### CRITICAL

**Definição:** Violação que quebra contrato, linhagem ou consistência fundamental.

**Ação:** BLOQUEIA MERGE

**Exemplos:**
- Inconsistência semântica (customer_id vs. id_customer em múltiplas tabelas)
- Chave estrangeira com padrão técnico (fk_customer)

**Regras:**
- `./rule-02-consistency.md` (inconsistência semântica)
- `./rule-08-foreign-keys.md` (padrão técnico)

**Procedimento:**
1. Detectar violação
2. Bloquear merge
3. Sinalizar para revisão humana
4. Exigir correção antes de prosseguir

---

### HIGH

**Definição:** Violação que reduz legibilidade, causa ambiguidade ou quebra padrão obrigatório.

**Ação:** REQUER REVISÃO

**Exemplos:**
- Formato incorreto (camelCase, maiúsculas, acentos)
- Unidade faltante em valor mensurável
- Abreviação proibida
- Tipo codificado em nome
- Data sem sufixo

**Regras:**
- `./rule-01-format.md` (formato)
- `./rule-03-units.md` (unidades)
- `./rule-04-abbreviations.md` (abreviações)
- `./rule-05-no-types.md` (tipos)
- `./rule-07-dates.md` (datas)

**Procedimento:**
1. Detectar violação
2. Sinalizar para revisão
3. Sugerir correção
4. Permitir auto-fix se determinístico
5. Exigir confirmação se ambíguo

---

### MEDIUM

**Definição:** Violação que afeta clareza ou padrão recomendado.

**Ação:** REQUER REVISÃO

**Exemplos:**
- Booleano sem prefixo
- Ordem de componentes incorreta
- Tipo codificado em nome (alternativa)

**Regras:**
- `./rule-06-booleans.md` (booleanos)
- `./rule-09-composition-order.md` (ordem)
- `./rule-05-no-types.md` (tipos - alternativa)

**Procedimento:**
1. Detectar violação
2. Sinalizar para revisão
3. Sugerir correção
4. Permitir auto-fix se tipo é confirmado
5. Exigir confirmação se ambíguo

---

### LOW

**Definição:** Violação que afeta especificidade ou recomendação.

**Ação:** RECOMENDAÇÃO

**Exemplos:**
- Nome genérico ou vago

**Regras:**
- `./rule-10-avoid-generic.md` (genericidade)

**Procedimento:**
1. Detectar violação
2. Sinalizar como recomendação
3. Sugerir alternativas
4. Permitir merge mesmo sem correção
5. Documentar racional se não corrigir

---

## Matriz de decisão

| Severidade | Bloqueia? | Auto-fix? | Requer confirmação? | Permite merge? |
|-----------|-----------|-----------|-------------------|----------------|
| CRITICAL | ✅ SIM | ❌ NÃO | ✅ SIM | ❌ NÃO |
| HIGH | ❌ NÃO | ✅ SIM (se determinístico) | ✅ SIM (se ambíguo) | ✅ SIM |
| MEDIUM | ❌ NÃO | ✅ SIM (condicional) | ✅ SIM (se ambíguo) | ✅ SIM |
| LOW | ❌ NÃO | ❌ NÃO | ❌ NÃO | ✅ SIM |

---

## Mapeamento: Regra → Severidade

| Regra | Severidade | Tipo |
|-------|-----------|------|
| rule-01-format.md | HIGH | Formato |
| rule-02-consistency.md | CRITICAL | Consistência |
| rule-03-units.md | HIGH | Unidades |
| rule-04-abbreviations.md | HIGH | Abreviações |
| rule-05-no-types.md | MEDIUM | Tipos |
| rule-06-booleans.md | MEDIUM | Booleanos |
| rule-07-dates.md | HIGH | Datas |
| rule-08-foreign-keys.md | CRITICAL | Chaves |
| rule-09-composition-order.md | MEDIUM | Ordem |
| rule-10-avoid-generic.md | LOW | Genericidade |

---

## Exemplo de aplicação

### Violação 1: Inconsistência semântica

```
Nome: id_customer (em tabela orders)
Referência: customer_id (em tabela customers)

Severidade: CRITICAL
Razão: Inconsistência semântica quebra linhagem
Ação: BLOQUEIA MERGE
Procedimento: Exigir renomeação para customer_id
```

---

### Violação 2: Formato incorreto

```
Nome: CustomerID
Esperado: customer_id

Severidade: HIGH
Razão: Violação de formato (camelCase)
Ação: REQUER REVISÃO
Procedimento: Auto-fix para customer_id
```

---

### Violação 3: Unidade faltante

```
Nome: weight
Esperado: weight_kg (ou weight_lb ou weight_oz)

Severidade: HIGH
Razão: Unidade ambígua
Ação: REQUER REVISÃO
Procedimento: Sinalizar para revisão humana, sugerir alternativas
```

---

### Violação 4: Booleano sem prefixo

```
Nome: active
Esperado: is_active

Severidade: MEDIUM
Razão: Ambíguo se é booleano
Ação: REQUER REVISÃO
Procedimento: Auto-fix se tipo é BOOLEAN confirmado
```

---

### Violação 5: Nome genérico

```
Nome: data
Esperado: customer_name, customer_email, etc.

Severidade: LOW
Razão: Muito vago
Ação: RECOMENDAÇÃO
Procedimento: Sugerir alternativas, permitir merge
```

---

## Limites

Este arquivo fornece tabela de referência de severidade.

Este arquivo não substitui:

- regras específicas
- política de naming
- padrão fundamental
