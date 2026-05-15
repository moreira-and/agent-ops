# semantic-naming-detection

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento operacional para detectar automaticamente violações de naming semântico em código, schemas e transformações.

Este arquivo é a fonte primária para técnica de detecção de violações de naming.

---

## Quando usar

Use esta skill quando precisar:

- escanear código para violações de naming
- identificar inconsistências semânticas
- gerar relatório de conformidade
- alimentar pipeline de validação
- estruturar detecção em CI/CD

---

## Quando não usar

Não use esta skill como fonte primária para:

- política de naming
- regras específicas
- validação manual
- correção automática
- prompts de enforcement

Consulte, respectivamente:

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `./semantic-naming-validation.md`
- `./semantic-naming-autofix.md`
- `../../prompts/review/enforce-semantic-naming.md`

---

## Dependências relacionadas

- `../../rules/naming/README.md` (roteador do conjunto de naming)
- `./semantic-naming-validation.md`

---

## Padrões de detecção

### Padrão 1: Violação de formato

**Detectar:** Nomes que não seguem `entity_detail_property_unit`

**Regex:**
```
^[A-Z]|[A-Z]|[^a-z0-9_]|__
```

**Exemplos detectados:**
```
customerId          # camelCase
CustomerName        # PascalCase
customer__id        # double underscore
customer-id         # hífen
customer.id         # ponto
```

---

### Padrão 2: Abreviações ambíguas

**Detectar:** Nomes contendo abreviações proibidas

**Lista de abreviações proibidas:**
```
dt, vlr, cod, qtd, desc, cust, prod, inv, addr, tel, doc, ref
```

**Regex:**
```
\b(dt|vlr|cod|qtd|desc|cust|prod|inv|addr|tel|doc|ref)_
```

**Exemplos detectados:**
```
dt_criacao
vlr_total
cod_cliente
qtd_items
desc_produto
```

---

### Padrão 3: Unidades faltantes

**Detectar:** Nomes de valores mensuráveis sem unidade

**Conceitos mensuráveis:**
```
weight, volume, temperature, distance, amount, price, duration, 
speed, pressure, density, concentration, percentage
```

**Regex:**
```
(weight|volume|temperature|distance|amount|price|duration|speed|pressure|density|concentration|percentage)(?!_[a-z]+)$
```

**Exemplos detectados:**
```
weight              # sem unidade
temperature         # sem unidade
amount              # sem unidade
price               # sem unidade
```

---

### Padrão 4: Tipos codificados em nomes

**Detectar:** Nomes contendo sufixos de tipo

**Sufixos de tipo:**
```
_int, _float, _string, _boolean, _timestamp, _date, _decimal
```

**Regex:**
```
_(int|float|string|boolean|timestamp|decimal)$
```

**Exemplos detectados:**
```
customer_id_int
amount_float
name_string
is_active_boolean
created_date_timestamp
```

---

### Padrão 5: Booleanos sem prefixo

**Detectar:** Colunas booleanas sem `is_` ou `has_`

**Contexto:** Requer análise de tipo de dado ou convenção de naming

**Exemplos detectados:**
```
active              # deveria ser is_active
deleted             # deveria ser is_deleted
primary             # deveria ser is_primary
address             # deveria ser has_address
```

---

### Padrão 6: Datas sem sufixo

**Detectar:** Colunas de data sem `_date` ou `_at`

**Contexto:** Requer análise de tipo de dado ou convenção de naming

**Exemplos detectados:**
```
created             # deveria ser created_at
updated             # deveria ser updated_at
birth                # deveria ser birth_date
```

---

### Padrão 7: Chaves estrangeiras com prefixo técnico

**Detectar:** Nomes de chaves estrangeiras usando `fk_` ou `id_<entity>`

**Regex:**
```
^fk_|^id_[a-z]
```

**Exemplos detectados:**
```
fk_customer         # deveria ser customer_id
id_customer         # deveria ser customer_id
fk_product          # deveria ser product_id
```

---

### Padrão 8: Inconsistência semântica

**Detectar:** Mesmo conceito com nomes diferentes

**Procedimento:**

1. Extrair entidades semânticas (customer, product, order, etc.)
2. Para cada entidade, coletar todos os nomes de coluna
3. Verificar se há variações (customer_id vs. id_customer vs. cod_customer)
4. Sinalizar inconsistências

**Exemplos detectados:**
```
Tabela A: customer_id
Tabela B: id_customer
Tabela C: cod_customer
→ Inconsistência semântica detectada
```

---

### Padrão 9: Nomes genéricos ou vagos

**Detectar:** Nomes que não comunicam significado específico

**Nomes genéricos:**
```
data, value, temp, var, result, output, x, y, z, item, thing, stuff
```

**Regex:**
```
^(data|value|temp|var|result|output|x|y|z|item|thing|stuff)$
```

**Exemplos detectados:**
```
data                # vago
value               # vago
temp                # vago
result              # vago
```

---

### Padrão 10: Idioma misto

**Detectar:** Nomes misturando português e inglês

**Procedimento:**

1. Manter dicionário de palavras em português
2. Manter dicionário de palavras em inglês
3. Verificar se nome contém palavras de ambos os idiomas

**Exemplos detectados:**
```
cod_cliente         # português + inglês
peso_kg             # português + inglês
data_creation       # português + inglês
```

---

## Algoritmo de detecção

```
Para cada nome em [colunas, variáveis, aliases]:
    
    1. Verificar padrão 1 (formato)
    2. Verificar padrão 2 (abreviações)
    3. Verificar padrão 3 (unidades)
    4. Verificar padrão 4 (tipos)
    5. Verificar padrão 5 (booleanos)
    6. Verificar padrão 6 (datas)
    7. Verificar padrão 7 (chaves)
    8. Verificar padrão 8 (inconsistência)
    9. Verificar padrão 9 (genericidade)
    10. Verificar padrão 10 (idioma)
    
    Se violação encontrada:
        Classificar severidade
        Documentar racional
        Sugerir alternativa
        Adicionar a relatório
```

---

## Saída de detecção

Estruturar como:

```json
{
  "violations": [
    {
      "name": "cod_cliente",
      "pattern": "abbreviation + mixed_language",
      "severity": "HIGH",
      "rule": "Regra 1, Regra 4",
      "reason": "Abreviação 'cod' + idioma misto português/inglês",
      "suggestion": "customer_id",
      "semantic_impact": "Reduz discoverabilidade, quebra consistência"
    }
  ],
  "summary": {
    "total_names": 10,
    "violations_found": 3,
    "critical": 0,
    "high": 2,
    "medium": 1,
    "low": 0
  }
}
```

---

## Limites

Esta skill fornece procedimento de detecção.

Esta skill não substitui:

- política de naming
- regras específicas
- validação manual
- correção automática
- prompts de enforcement

---

## Relação com demais artefatos

- referencia `../../rules/naming/README.md`
- referencia regras específicas selecionadas pelo roteador de naming
- referencia `../../rules/naming/reference-units.md`
- referencia `../../rules/naming/reference-severity.md`
- complementa `./semantic-naming-validation.md`
- alimenta `./semantic-naming-autofix.md`
- é acionada por `../../prompts/review/enforce-semantic-naming.md`
