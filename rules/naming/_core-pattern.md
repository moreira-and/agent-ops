# _core-pattern

## Tipo do artefato

rule

## Finalidade

Definir o padrão fundamental de nomenclatura semântica que governa todas as 10 regras.

Este arquivo é a fonte primária para o padrão core de naming.

---

## Quando usar

Use este arquivo quando precisar:

- entender o padrão fundamental de naming
- validar se um nome segue estrutura básica
- orientar decomposição de nomes complexos
- estabelecer base para todas as outras regras

---

## Quando não usar

Não use este arquivo como fonte primária para:

- regras específicas de formato
- regras de consistência
- regras de unidades
- regras de abreviações

Consulte, respectivamente:

- `./rule-01-format.md`
- `./rule-02-consistency.md`
- `./rule-03-units.md`
- `./rule-04-abbreviations.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `./README.md`

---

## Padrão fundamental

### Estrutura

```
entity_detail_property_unit
```

### Componentes

#### **entity** (obrigatório)
Conceito semântico principal que o nome representa.

**Exemplos:**
- customer
- product
- order
- invoice
- employee
- department

**Características:**
- Singular (customer, não customers)
- Substantivo concreto
- Representa a entidade primária

---

#### **detail** (opcional)
Refinamento ou contexto que qualifica a entidade.

**Exemplos:**
- billing (customer_billing_address)
- shipping (customer_shipping_address)
- primary (customer_primary_contact)
- secondary (customer_secondary_contact)
- net (product_net_weight_kg)
- gross (product_gross_weight_kg)
- unit (product_unit_price_brl)
- total (product_total_price_brl)

**Características:**
- Qualifica ou refina a entidade
- Adiciona contexto semântico
- Opcional (nem todo nome precisa)

---

#### **property** (obrigatório)
Atributo, medida ou característica sendo nomeada.

**Exemplos:**
- name
- email
- phone
- address
- weight
- price
- amount
- date
- count
- status

**Características:**
- Descreve o que está sendo medido/armazenado
- Substantivo ou adjetivo descritivo
- Sempre presente

---

#### **unit** (condicional)
Unidade de medida para valores mensuráveis.

**Exemplos:**
- kg (weight_kg)
- brl (price_brl)
- celsius (temperature_celsius)
- m (distance_m)
- percent (discount_percent)

**Características:**
- Obrigatório para valores mensuráveis
- Opcional para valores não-mensuráveis
- Sempre no final do nome

---

## Exemplos de decomposição

### Exemplo 1: Simples
```
customer_name

Decomposição:
- entity: customer
- detail: (nenhum)
- property: name
- unit: (nenhum)
```

### Exemplo 2: Com detail
```
customer_billing_address

Decomposição:
- entity: customer
- detail: billing
- property: address
- unit: (nenhum)
```

### Exemplo 3: Com unidade
```
product_net_weight_kg

Decomposição:
- entity: product
- detail: net
- property: weight
- unit: kg
```

### Exemplo 4: Complexo
```
order_line_item_quantity

Decomposição:
- entity: order
- detail: line_item
- property: quantity
- unit: (nenhum)
```

---

## Restrições globais

Todas as regras específicas respeitam estas restrições:

### Formato
- MUST usar snake_case
- MUST usar lowercase
- MUST NOT conter acentos
- MUST NOT conter espaços
- MUST NOT conter caracteres especiais (exceto underscore)

### Semântica
- MUST ser determinístico (mesmo conceito = sempre mesmo nome)
- MUST ser específico (não genérico)
- MUST comunicar significado

### Estrutura
- MUST seguir ordem: entity → detail → property → unit
- MUST NOT inverter ordem
- MUST NOT omitir componentes obrigatórios

---

## Validação do padrão

Para validar se um nome segue o padrão:

1. **Decompor** o nome em componentes
2. **Verificar** se cada componente está no lugar correto
3. **Validar** restrições globais
4. **Confirmar** que componentes obrigatórios estão presentes

### Exemplo de validação

**Nome:** `customer_billing_address`

```
1. Decompor:
   - customer (entity) ✓
   - billing (detail) ✓
   - address (property) ✓
   - (nenhum unit) ✓

2. Verificar ordem:
   - entity → detail → property → unit ✓

3. Validar restrições:
   - snake_case ✓
   - lowercase ✓
   - sem acentos ✓
   - sem espaços ✓
   - sem caracteres especiais ✓

4. Confirmar obrigatórios:
   - entity presente ✓
   - property presente ✓

Resultado: ✅ VÁLIDO
```

---

## Relação com demais regras

Este padrão é a base para:

- `./rule-01-format.md` - Implementa restrições de formato
- `./rule-02-consistency.md` - Garante mesmo padrão em múltiplas tabelas
- `./rule-03-units.md` - Define quando unit é obrigatório
- `./rule-04-abbreviations.md` - Restringe componentes
- `./rule-05-no-types.md` - Proíbe tipos em componentes
- `./rule-06-booleans.md` - Padrão especial para booleanos
- `./rule-07-dates.md` - Padrão especial para datas
- `./rule-08-foreign-keys.md` - Padrão especial para chaves
- `./rule-09-composition-order.md` - Ordem de componentes
- `./rule-10-avoid-generic.md` - Especificidade de componentes

---

## Limites

Este arquivo define o padrão fundamental.

Este arquivo não substitui:

- regras específicas de formato
- regras de consistência
- regras de unidades
- regras de abreviações
- regras de tipos
- regras especiais (booleanos, datas, chaves)

---

## Uso pelo agente

Ao consumir este arquivo, o agente deve:

- entender que é a base para todas as outras regras
- usar decomposição para validar nomes
- respeitar ordem: entity → detail → property → unit
- aplicar restrições globais
- referenciar regras específicas para casos especiais
