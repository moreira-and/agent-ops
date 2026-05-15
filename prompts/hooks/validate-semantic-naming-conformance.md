# validate-semantic-naming-conformance

## Tipo do artefato

hook prompt

## Finalidade

Definir checkpoint de validação para conformidade de naming semântico antes de conclusão de tarefa ou merge.

---

## Quando usar

Use este hook quando precisar:

- validar conformidade antes de merge
- revisar naming antes de deploy
- auditar consistência antes de conclusão
- bloquear violações críticas
- documentar conformidade

---

## Quando não usar

Não use este hook como fonte primária para:

- política de naming
- regras específicas
- procedimentos de validação
- procedimentos de detecção
- procedimentos de auto-fix

Consulte, respectivamente:

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Dependências relacionadas

- `../../governance/composition/semantic-naming-governance.md`
- `../../rules/naming/README.md`
- `../../rules/naming/reference-units.md`
- `../../rules/naming/reference-severity.md`
- `../../skills/review/semantic-naming-validation.md`

---

## Momento de uso

Este hook SHOULD ser acionado:

- **Antes de merge:** Validar conformidade de naming
- **Antes de deploy:** Auditar consistência
- **Antes de conclusão:** Revisar aderência

---

## Instrução operacional

Ao usar este hook, o agente SHOULD:

1. Carregar `../../rules/naming/README.md`
2. Carregar apenas as regras específicas indicadas pelo roteador de naming
3. Carregar `../../rules/naming/reference-units.md` e `../../rules/naming/reference-severity.md`
4. Carregar `../../governance/composition/semantic-naming-governance.md`
5. Executar validação de conformidade
6. Classificar violações por severidade
7. Bloquear se violações CRITICAL ou HIGH existem
8. Documentar resultado

---

## Checklist de validação

Antes de prosseguir, validar:

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

## Critério de bloqueio

### Bloqueia merge se:

- Violação CRITICAL existe (inconsistência semântica)
- Violação HIGH existe sem racional documentado
- Ambiguidade semântica não foi resolvida

### Permite merge se:

- Todas as violações CRITICAL foram resolvidas
- Todas as violações HIGH têm racional documentado
- Ambiguidades foram explicitamente confirmadas

---

## Saída esperada

O hook SHOULD produzir:

```
CONFORMANCE VALIDATION RESULT
=============================

Status: [PASS | FAIL | CONDITIONAL]

Violations found: [número]
- CRITICAL: [número]
- HIGH: [número]
- MEDIUM: [número]
- LOW: [número]

Details:
[lista de violações com racional]

Recommendation:
[APPROVE | BLOCK | REQUIRES_REVIEW]
```

---

## Exemplo de execução

### Input

```
Schema para validar:
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(255),
    weight_kg DECIMAL(10,2),
    created_at TIMESTAMP,
    is_active BOOLEAN
);
```

### Execução

```
CONFORMANCE VALIDATION RESULT
=============================

Status: PASS

Violations found: 0
- CRITICAL: 0
- HIGH: 0
- MEDIUM: 0
- LOW: 0

Details:
✓ customer_id: Segue padrão
✓ customer_name: Segue padrão
✓ weight_kg: Unidade presente
✓ created_at: Padrão de timestamp
✓ is_active: Prefixo booleano

Recommendation: APPROVE
```

---

### Exemplo com violações

### Input

```
Schema para validar:
CREATE TABLE orders (
    id_order INT,
    fk_customer INT,
    vlr_total DECIMAL(10,2),
    data_criacao TIMESTAMP,
    ativo BOOLEAN
);
```

### Execução

```
CONFORMANCE VALIDATION RESULT
=============================

Status: FAIL

Violations found: 5
- CRITICAL: 1
- HIGH: 3
- MEDIUM: 1
- LOW: 0

Details:

[CRITICAL]
fk_customer: Inconsistência semântica
Regra violada: Regra 8 (chaves estrangeiras)
Razão: Usa prefixo técnico em vez de padrão semântico
Sugestão: customer_id
Impacto: Quebra consistência com tabela customers
Ação: BLOQUEIA MERGE

[HIGH]
id_order: Formato invertido
Regra violada: Regra 1 (formato)
Razão: Ordem invertida (id_entity em vez de entity_id)
Sugestão: order_id
Impacto: Reduz discoverabilidade
Ação: REQUER REVISÃO

[HIGH]
vlr_total: Abreviação + unidade faltante
Regra violada: Regra 3, Regra 4
Razão: Abreviação "vlr" + unidade ambígua
Sugestão: total_amount_brl (ou total_amount_usd?)
Impacto: Ambíguo, impede raciocínio automatizado
Ação: REQUER REVISÃO

[HIGH]
data_criacao: Abreviação + idioma misto
Regra violada: Regra 4, Regra 7
Razão: Abreviação "dt" + idioma misto português/inglês
Sugestão: created_at
Impacto: Reduz legibilidade
Ação: REQUER REVISÃO

[MEDIUM]
ativo: Booleano sem prefixo
Regra violada: Regra 6
Razão: Coluna booleana sem prefixo is_/has_
Sugestão: is_active
Impacto: Ambíguo se é booleano ou string
Ação: REQUER REVISÃO

Recommendation: BLOCK
Razão: Violação CRITICAL encontrada (inconsistência semântica)
Ação necessária: Resolver fk_customer antes de merge
```

---

## Limites

Este hook valida conformidade de naming.

Este hook não substitui:

- política de naming
- regras específicas
- procedimentos de validação
- procedimentos de detecção
- procedimentos de auto-fix

---

## Relação com demais artefatos

- valida contra `../../rules/naming/_core-pattern.md`
- valida contra as regras selecionadas via `../../rules/naming/README.md`
- valida contra `../../rules/naming/reference-units.md`
- valida contra `../../rules/naming/reference-severity.md`
- valida contra `../../governance/composition/semantic-naming-governance.md`
- é acionado por `../review/enforce-semantic-naming.md`
