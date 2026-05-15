# rule-03-units

## Tipo do artefato

rule

## Finalidade

Definir obrigatoriedade de unidades explícitas para valores mensuráveis.

---

## Quando usar

Use esta regra quando precisar:

- validar se valores mensuráveis têm unidade
- identificar ambiguidade de unidades
- revisar conformidade de nomes de medidas
- implementar linter de unidades

---

## Quando não usar

Não use esta regra como fonte primária para:

- padrão fundamental
- formato de nomes
- consistência semântica
- abreviações

Consulte, respectivamente:

- `./_core-pattern.md`
- `./rule-01-format.md`
- `./rule-02-consistency.md`
- `./rule-04-abbreviations.md`

---

## Dependências relacionadas

- `./_core-pattern.md`

---

## Regra

**Princípio:** Toda coluna representando quantidade, peso, volume, temperatura, moeda, etc. MUST declarar unidade explicitamente.

### Aplicação

Valores mensuráveis MUST incluir unidade no nome.

---

## Conceitos mensuráveis

| Conceito | Exemplos | Unidades válidas |
|----------|----------|------------------|
| Peso | weight, mass | kg, g, lb, oz |
| Volume | volume, capacity | l, ml, m3, gallon |
| Temperatura | temperature, temp | celsius, fahrenheit, kelvin |
| Distância | distance, length | m, km, cm, mile |
| Moeda | amount, price, cost | brl, usd, eur, gbp |
| Tempo | duration, elapsed | seconds, minutes, hours, days |
| Percentual | percentage, ratio | percent, pct |
| Velocidade | speed, velocity | kmh, mph, ms |
| Pressão | pressure | pa, bar, psi |
| Densidade | density | kgm3, gcm3 |
| Concentração | concentration | ppm, percent |

---

## Exemplos de conformidade

### Exemplo 1: Correto

**Conceito:** weight (peso)

```
weight_kg           ✅ (unidade explícita)
weight_g            ✅ (unidade explícita)
weight_lb           ✅ (unidade explícita)
```

**Validação:**
- Valor mensurável? ✅
- Unidade presente? ✅
- Unidade válida? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 2: Incorreto

**Conceito:** weight (peso)

```
weight              ❌ (qual unidade?)
peso                ❌ (qual unidade?)
weight_value        ❌ (qual unidade?)
```

**Validação:**
- Valor mensurável? ✅
- Unidade presente? ❌

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** weight_kg (ou weight_g, weight_lb)

---

### Exemplo 3: Correto

**Conceito:** amount (valor monetário)

```
amount_brl          ✅ (moeda explícita)
amount_usd          ✅ (moeda explícita)
amount_eur          ✅ (moeda explícita)
```

**Validação:**
- Valor mensurável? ✅
- Unidade presente? ✅
- Unidade válida? ✅

**Resultado:** ✅ VÁLIDO

---

### Exemplo 4: Incorreto

**Conceito:** amount (valor monetário)

```
amount              ❌ (qual moeda?)
vlr_total           ❌ (qual moeda?)
total               ❌ (qual moeda?)
```

**Validação:**
- Valor mensurável? ✅
- Unidade presente? ❌

**Resultado:** ❌ VIOLAÇÃO

**Sugestão:** amount_brl (ou amount_usd, amount_eur)

---

## Severidade

**Severidade:** HIGH

Falta de unidade causa:
- Ambiguidade semântica
- Impossibilidade de raciocínio automatizado
- Erros de conversão
- Confusão em análises

---

## Auto-fix bloqueado

Adicionar unidade automaticamente é BLOQUEADO.

**Razão:** Unidade pode ser ambígua (weight pode ser kg, lb, oz).

**Procedimento:**
1. Detectar valor mensurável sem unidade
2. Sinalizar para revisão humana
3. Sugerir alternativas
4. Solicitar confirmação

---

## Procedimento de validação

### Passo 1: Identificar valores mensuráveis

Listar todas as colunas que representam medidas:

```
Colunas mensuráveis:
- weight
- temperature
- distance
- amount
- duration
- pressure
```

---

### Passo 2: Para cada coluna, verificar unidade

```
Validação:
- weight: tem unidade? ❌
- temperature: tem unidade? ❌
- distance: tem unidade? ❌
- amount: tem unidade? ❌
- duration: tem unidade? ❌
- pressure: tem unidade? ❌
```

---

### Passo 3: Se falta unidade, sinalizar

```
Violações encontradas:
1. weight (deveria ser weight_kg ou weight_lb ou weight_oz)
2. temperature (deveria ser temperature_celsius ou temperature_fahrenheit)
3. distance (deveria ser distance_m ou distance_km ou distance_mile)
4. amount (deveria ser amount_brl ou amount_usd ou amount_eur)
5. duration (deveria ser duration_seconds ou duration_minutes ou duration_hours)
6. pressure (deveria ser pressure_pa ou pressure_bar ou pressure_psi)
```

---

## Exemplo de detecção

### Input

```sql
CREATE TABLE products (
    product_id INT,
    weight DECIMAL(10,2),
    volume DECIMAL(10,2),
    price DECIMAL(10,2),
    temperature DECIMAL(10,2)
);
```

### Detecção

```
Colunas mensuráveis sem unidade:
1. weight (qual unidade? kg? lb? oz?)
2. volume (qual unidade? l? ml? gallon?)
3. price (qual moeda? brl? usd? eur?)
4. temperature (qual escala? celsius? fahrenheit?)

Severidade: HIGH
Ação: REQUER REVISÃO
```

---

## Unidades comuns por conceito

### Peso
```
kg      (quilograma)
g       (grama)
lb      (libra)
oz      (onça)
```

### Volume
```
l       (litro)
ml      (mililitro)
m3      (metro cúbico)
gallon  (galão)
```

### Temperatura
```
celsius     (Celsius)
fahrenheit  (Fahrenheit)
kelvin      (Kelvin)
```

### Distância
```
m       (metro)
km      (quilômetro)
cm      (centímetro)
mile    (milha)
```

### Moeda
```
brl     (Real Brasileiro)
usd     (Dólar Americano)
eur     (Euro)
gbp     (Libra Esterlina)
```

### Tempo
```
seconds     (segundos)
minutes     (minutos)
hours       (horas)
days        (dias)
```

---

## Limites

Esta regra governa unidades em valores mensuráveis.

Esta regra não governa:

- padrão fundamental
- formato de nomes
- consistência semântica
- abreviações
- tipos
- casos especiais

---

## Relação com demais artefatos

- referencia `./_core-pattern.md`
- é validada por `../../skills/review/semantic-naming-validation.md`
- é detectada por `../../skills/review/semantic-naming-detection.md` (padrão 3)
- é bloqueada por `../../skills/review/semantic-naming-autofix.md` (não auto-fix)
