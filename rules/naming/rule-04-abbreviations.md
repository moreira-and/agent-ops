# rule-04-abbreviations

## Tipo do artefato

rule

## Finalidade

Definir quais abreviações são permitidas e quais são proibidas em nomes semânticos.

---

## Quando usar

Use esta regra quando precisar:

- validar se um nome usa abreviações permitidas
- identificar abreviações proibidas
- revisar conformidade de nomenclatura
- implementar linter de abreviações

---

## Quando não usar

Não use esta regra como fonte primária para:

- padrão fundamental
- formato de nomes
- consistência semântica
- unidades

Consulte, respectivamente:

- `./_core-pattern.md`
- `./rule-01-format.md`
- `./rule-02-consistency.md`
- `./rule-03-units.md`

---

## Dependências relacionadas

- `./_core-pattern.md`

---

## Regra

**Princípio:** Abreviações reduzem legibilidade e aumentam ambiguidade. Apenas abreviações universalmente reconhecidas são permitidas.

---

## Abreviações proibidas

| Proibido | Correto | Razão |
|----------|---------|-------|
| dt | date | Ambíguo (data? datetime?) |
| vlr | amount | Ambíguo (valor? volume?) |
| cod | code | Ambíguo (código? codificação?) |
| qtd | quantity | Ambíguo (quantidade? qualidade?) |
| desc | description | Ambíguo (descrição? desconto?) |
| cust | customer | Ambíguo (cliente? customização?) |
| prod | product | Ambíguo (produto? produção?) |
| inv | invoice | Ambíguo (fatura? inventário?) |
| addr | address | Ambíguo (endereço? addressee?) |
| tel | phone | Ambíguo (telefone? telemetria?) |
| doc | document | Ambíguo (documento? docking?) |
| ref | reference | Ambíguo (referência? refund?) |
| val | value | Ambíguo (valor? validação?) |
| num | number | Ambíguo (número? numérico?) |
| seq | sequence | Ambíguo (sequência? sequencial?) |
| max | maximum | Ambíguo (máximo? maximal?) |
| min | minimum | Ambíguo (mínimo? minimal?) |
| avg | average | Ambíguo (média? averaging?) |
| cnt | count | Ambíguo (contagem? contador?) |
| pct | percent | Use percent ou percentage |
| amt | amount | Use amount |

---

## Abreviações permitidas

Apenas quando universalmente reconhecidas:

### Identificadores
```
id      (identifier - universalmente reconhecido)
```

**Uso permitido:**
```
customer_id         ✅
product_id          ✅
order_id            ✅
```

---

### Chaves (apenas em contexto de schema)
```
fk      (foreign key - apenas em contexto técnico)
pk      (primary key - apenas em contexto técnico)
```

**Uso permitido:**
```
-- Em contexto de schema/DDL:
CONSTRAINT fk_customer FOREIGN KEY (customer_id)
PRIMARY KEY pk_orders (order_id)
```

**Uso NÃO permitido em nomes semânticos:**
```
fk_customer         ❌ (use customer_id)
pk_order            ❌ (use order_id)
```

---

### Moedas (ISO 4217)
```
brl     (Real Brasileiro)
usd     (Dólar Americano)
eur     (Euro)
gbp     (Libra Esterlina)
jpy     (Iene Japonês)
cad     (Dólar Canadense)
aud     (Dólar Australiano)
```

**Uso permitido:**
```
amount_brl          ✅
price_usd           ✅
cost_eur            ✅
```

---

### Unidades SI
```
kg      (quilograma)
g       (grama)
m       (metro)
km      (quilômetro)
cm      (centímetro)
l       (litro)
ml      (mililitro)
```

**Uso permitido:**
```
weight_kg           ✅
distance_m          ✅
volume_l            ✅
```

---

## Severidade

**Severidade:** HIGH

Abreviações ambíguas causam:
- Redução de legibilidade
- Aumento de ambiguidade
- Dificuldade de manutenção
- Erros de interpretação

---

## Auto-fix permitido

Transformações automáticas permitidas:

- dt → date
- vlr → amount
- cod → code
- qtd → quantity
- desc → description
- cust → customer
- prod → product
- inv → invoice
- addr → address
- tel → phone
- doc → document
- ref → reference

---

## Procedimento de validação

### Passo 1: Extrair componentes do nome

```
Nome: cod_cliente_endereco

Componentes:
- cod (abreviação)
- cliente (palavra completa)
- endereco (palavra completa)
```

---

### Passo 2: Para cada componente, verificar se é abreviação

```
Validação:
- cod: é abreviação? ✅ (proibida)
- cliente: é abreviação? ❌
- endereco: é abreviação? ❌
```

---

### Passo 3: Se houver abreviação proibida, sinalizar

```
Violações encontradas:
1. cod (deveria ser code)

Sugestão: code_customer_address
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE customers (
    cod_cliente INT,
    desc_cliente VARCHAR(255),
    tel_cliente VARCHAR(20),
    addr_cliente VARCHAR(255)
);
```

### Detecção

```
Abreviações proibidas encontradas:
1. cod_cliente (deveria ser code_customer ou customer_code)
2. desc_cliente (deveria ser description_customer ou customer_description)
3. tel_cliente (deveria ser phone_customer ou customer_phone)
4. addr_cliente (deveria ser address_customer ou customer_address)

Severidade: HIGH
Ação: REQUER REVISÃO
```

---

## Exemplo de auto-fix

### Input

```
dt_criacao
vlr_total
cod_produto
qtd_items
```

### Auto-fix

```
dt_criacao → created_at (ou created_date)
vlr_total → total_amount
cod_produto → product_code
qtd_items → item_quantity
```

---

## Limites

Esta regra governa abreviações.

Esta regra não governa:

- padrão fundamental
- formato de nomes
- consistência semântica
- unidades
- tipos
- casos especiais

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 2)
- é corrigida por `../../skills/review/semantic-naming-autofix.md` (transformação 4)
