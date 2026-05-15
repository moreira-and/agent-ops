# reference-units

## Tipo do artefato

rule

## Finalidade

Fornecer tabela de referência de unidades válidas para valores mensuráveis.

---

## Quando usar

Use este arquivo quando precisar:

- validar se unidade é válida
- escolher unidade apropriada
- padronizar unidades em domínio
- implementar linter de unidades

---

## Quando não usar

Não use este arquivo como fonte primária para:

- regra de unidades
- política de naming
- padrão fundamental

Consulte, respectivamente:

- `./rule-03-units.md`
- `../../governance/composition/semantic-naming-governance.md`
- `./_core-pattern.md`

---

## Dependências relacionadas

- `./rule-03-units.md`

---

## Unidades por conceito

### Peso

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Quilograma | kg | Padrão SI | weight_kg |
| Grama | g | Pequenas quantidades | weight_g |
| Libra | lb | Países anglo-saxões | weight_lb |
| Onça | oz | Países anglo-saxões | weight_oz |

---

### Volume

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Litro | l | Padrão SI | volume_l |
| Mililitro | ml | Pequenas quantidades | volume_ml |
| Metro cúbico | m3 | Grandes quantidades | volume_m3 |
| Galão | gallon | Países anglo-saxões | volume_gallon |

---

### Temperatura

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Celsius | celsius | Padrão internacional | temperature_celsius |
| Fahrenheit | fahrenheit | Países anglo-saxões | temperature_fahrenheit |
| Kelvin | kelvin | Contexto científico | temperature_kelvin |

---

### Distância

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Metro | m | Padrão SI | distance_m |
| Quilômetro | km | Distâncias longas | distance_km |
| Centímetro | cm | Pequenas distâncias | distance_cm |
| Milha | mile | Países anglo-saxões | distance_mile |

---

### Moeda

| Unidade | Código | País | Exemplo |
|---------|--------|------|---------|
| Real Brasileiro | brl | Brasil | amount_brl |
| Dólar Americano | usd | EUA | amount_usd |
| Euro | eur | Europa | amount_eur |
| Libra Esterlina | gbp | Reino Unido | amount_gbp |
| Iene Japonês | jpy | Japão | amount_jpy |
| Dólar Canadense | cad | Canadá | amount_cad |
| Dólar Australiano | aud | Austrália | amount_aud |
| Franco Suíço | chf | Suíça | amount_chf |

---

### Tempo

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Segundo | seconds | Padrão SI | duration_seconds |
| Minuto | minutes | Uso comum | duration_minutes |
| Hora | hours | Uso comum | duration_hours |
| Dia | days | Uso comum | duration_days |
| Semana | weeks | Períodos longos | duration_weeks |
| Mês | months | Períodos longos | duration_months |
| Ano | years | Períodos muito longos | duration_years |

---

### Percentual

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Percentual | percent | Padrão | discount_percent |
| Percentual (abreviado) | pct | Alternativa | discount_pct |

---

### Velocidade

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Quilômetro por hora | kmh | Padrão internacional | speed_kmh |
| Milha por hora | mph | Países anglo-saxões | speed_mph |
| Metro por segundo | ms | Contexto científico | speed_ms |

---

### Pressão

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Pascal | pa | Padrão SI | pressure_pa |
| Bar | bar | Uso industrial | pressure_bar |
| PSI | psi | Países anglo-saxões | pressure_psi |

---

### Densidade

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Quilograma por metro cúbico | kgm3 | Padrão SI | density_kgm3 |
| Grama por centímetro cúbico | gcm3 | Uso comum | density_gcm3 |

---

### Concentração

| Unidade | Código | Uso | Exemplo |
|---------|--------|-----|---------|
| Partes por milhão | ppm | Padrão | concentration_ppm |
| Percentual | percent | Alternativa | concentration_percent |

---

## Recomendações

### Preferência por padrão SI

Quando possível, usar unidades do Sistema Internacional (SI):

- Peso: kg
- Volume: l
- Temperatura: celsius
- Distância: m
- Tempo: seconds

### Contexto regional

Considerar contexto regional:

- Brasil: brl, kg, celsius, m
- EUA: usd, lb, fahrenheit, mile
- Europa: eur, kg, celsius, m

### Consistência em domínio

Manter consistência dentro de um domínio:

```
Domínio: e-commerce Brasil
- Moeda: brl (sempre)
- Peso: kg (sempre)
- Temperatura: celsius (sempre)
```

---

## Limites

Este arquivo fornece tabela de referência.

Este arquivo não substitui:

- regra de unidades
- política de naming
- padrão fundamental
