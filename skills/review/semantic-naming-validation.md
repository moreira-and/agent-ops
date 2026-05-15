# semantic-naming-validation

## Tipo do artefato

skill

## Finalidade

Fornecer procedimento operacional para validar conformidade de nomes contra regras de naming semântico.

Este arquivo é a fonte primária para técnica de validação de naming.

---

## Quando usar

Use esta skill quando precisar:

- validar se um conjunto de nomes segue padrão
- revisar conformidade antes de merge
- estruturar validação em pipeline
- orientar revisão manual de naming

---

## Quando não usar

Não use esta skill como fonte primária para:

- política de naming
- regras específicas
- detecção automática
- correção automática
- prompts de enforcement

Consulte, respectivamente:

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `./semantic-naming-detection.md`
- `./semantic-naming-autofix.md`
- `../../prompts/review/enforce-semantic-naming.md`

---

## Dependências relacionadas

- `../../rules/naming/README.md` (roteador do conjunto de naming)
- `../../rules/naming/reference-severity.md` (tabela de severidade)
- `../../governance/composition/semantic-naming-governance.md`

---

## Procedimento de validação

### Passo 1: Coletar nomes

Extrair todos os nomes de:

- colunas em SQL models
- colunas em DataFrames
- variáveis em transformações
- aliases em joins
- tabelas derivadas

### Passo 2: Validar formato

Para cada nome, verificar:

1. **Padrão:** Segue `entity_detail_property_unit`?
2. **Case:** É snake_case?
3. **Caracteres:** Apenas lowercase + underscore?
4. **Acentos:** Sem acentos?
5. **Espaços:** Sem espaços?

### Passo 3: Validar semântica

Para cada nome, verificar:

1. **Consistência:** Mesmo conceito usa sempre mesmo nome?
2. **Unidades:** Valores mensuráveis têm unidade?
3. **Abreviações:** Usa apenas abreviações permitidas?
4. **Tipos:** Não codifica tipo de dado?
5. **Booleanos:** Usa `is_` ou `has_`?
6. **Datas:** Usa `_date` ou `_at`?
7. **Chaves:** Chaves estrangeiras usam `<entity>_id`?
8. **Hierarquia:** Nomes compostos ordenados corretamente?
9. **Genericidade:** Nomes são específicos?

### Passo 4: Classificar violações

Para cada violação encontrada:

1. Identificar tipo de violação
2. Classificar severidade (CRITICAL, HIGH, MEDIUM, LOW)
3. Documentar racional
4. Sugerir alternativa

### Passo 5: Gerar relatório

Estruturar saída como:

```
[SEVERIDADE]
Nome atual: <current_name>
Regra violada: <rule_number>
Razão: <explanation>
Sugestão: <suggested_name>
Impacto: <semantic_impact>
```

---

## Checklist de validação

Use este checklist para validação manual:

- [ ] Todos os nomes seguem `entity_detail_property_unit`?
- [ ] Todos os nomes são snake_case?
- [ ] Todos os nomes são lowercase?
- [ ] Nenhum nome tem acentos?
- [ ] Nenhum nome tem espaços?
- [ ] Mesmo conceito sempre usa mesmo nome?
- [ ] Valores mensuráveis têm unidade?
- [ ] Nenhuma abreviação ambígua?
- [ ] Nenhum tipo codificado em nome?
- [ ] Booleanos usam `is_` ou `has_`?
- [ ] Datas usam `_date` ou `_at`?
- [ ] Chaves estrangeiras usam `<entity>_id`?
- [ ] Nomes compostos ordenados por hierarquia?
- [ ] Nenhum nome genérico ou vago?

---

## Exemplo de validação

### Input

```sql
CREATE TABLE customers (
    cod_cliente INT,
    nome VARCHAR(255),
    email VARCHAR(255),
    peso DECIMAL(10,2),
    dt_criacao TIMESTAMP,
    ativo BOOLEAN
);

CREATE TABLE orders (
    id_order INT,
    fk_customer INT,
    vlr_total DECIMAL(10,2),
    data_criacao TIMESTAMP
);
```

### Validação

| Nome | Regra | Severidade | Sugestão | Razão |
|------|-------|-----------|----------|-------|
| cod_cliente | 1, 4 | HIGH | customer_id | Abreviação + idioma misto |
| peso | 3 | HIGH | weight_kg | Unidade faltante |
| dt_criacao | 4, 7 | HIGH | created_at | Abreviação + padrão de data |
| ativo | 6 | MEDIUM | is_active | Booleano sem prefixo |
| id_order | 1 | MEDIUM | order_id | Ordem invertida |
| fk_customer | 8 | HIGH | customer_id | Padrão de chave estrangeira |
| vlr_total | 4 | HIGH | total_amount_brl | Abreviação + unidade faltante |
| data_criacao | 4, 7 | HIGH | created_at | Abreviação + idioma misto |

### Output

```
[HIGH]
Nome atual: cod_cliente
Regra violada: Regra 1 (formato), Regra 4 (abreviações)
Razão: Usa abreviação "cod" + idioma misto português/inglês
Sugestão: customer_id
Impacto semântico: Reduz discoverabilidade, quebra consistência com outras tabelas

[HIGH]
Nome atual: peso
Regra violada: Regra 3 (unidades)
Razão: Valor mensurável sem unidade explícita
Sugestão: weight_kg
Impacto semântico: Ambíguo (kg? lb? oz?), impede raciocínio automatizado

[HIGH]
Nome atual: dt_criacao
Regra violada: Regra 4 (abreviações), Regra 7 (datas)
Razão: Abreviação "dt" + idioma misto + não segue padrão de data
Sugestão: created_at
Impacto semântico: Reduz legibilidade, quebra padrão de timestamps

[MEDIUM]
Nome atual: ativo
Regra violada: Regra 6 (booleanos)
Razão: Coluna booleana sem prefixo is_/has_
Sugestão: is_active
Impacto semântico: Ambíguo se é booleano ou string

[HIGH]
Nome atual: fk_customer
Regra violada: Regra 8 (chaves estrangeiras)
Razão: Usa prefixo técnico "fk_" em vez de padrão semântico
Sugestão: customer_id
Impacto semântico: Reduz consistência com tabela referenciada
```

---

## Limites

Esta skill fornece procedimento de validação.

Esta skill não substitui:

- política de naming
- regras específicas
- detecção automática
- correção automática
- prompts de enforcement

---

## Relação com demais artefatos

- referencia `../../rules/naming/README.md`
- referencia regras específicas selecionadas pelo roteador de naming
- referencia `../../rules/naming/reference-units.md`
- referencia `../../rules/naming/reference-severity.md`
- referencia `../../governance/composition/semantic-naming-governance.md`
- complementa `./semantic-naming-detection.md`
- precede `./semantic-naming-autofix.md`
- é acionada por `../../prompts/review/enforce-semantic-naming.md`
