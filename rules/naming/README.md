# naming

## Tipo do artefato

discovery

## Finalidade

O diretório `naming/` define convenções de nomenclatura semântica para artefatos produzidos por agentes em ambientes de engenharia de dados.

`naming/` é a fonte primária para padrões de naming semântico.

A norma de maior precedência continua sendo:

- `../../MANIFEST.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../README.md`
- `../../governance/composition/semantic-naming-governance.md`

---

## Quando usar

Consulte `naming/` quando precisar:

- nomear artefatos (colunas, variáveis, aliases, etc.)
- revisar consistência de nomenclatura
- reduzir ambiguidade por nomes
- padronizar identificadores relevantes
- validar conformidade de naming

---

## Quando não usar

Não use `naming/` como fonte primária para:

- governança estrutural
- arquitetura
- implementação
- modelagem
- qualidade geral
- política de naming

Consulte, respectivamente:

- `../../governance/`
- `../architecture/`
- `../coding/`
- `../modeling/`
- `../quality/`
- `../../governance/composition/semantic-naming-governance.md`

---

## Estrutura interna

```txt
naming/
├── README.md
├── _core-pattern.md
├── rule-01-format.md
├── rule-02-consistency.md
├── rule-03-units.md
├── rule-04-abbreviations.md
├── rule-05-no-types.md
├── rule-06-booleans.md
├── rule-07-dates.md
├── rule-08-foreign-keys.md
├── rule-09-composition-order.md
├── rule-10-avoid-generic.md
├── reference-units.md
└── reference-severity.md
```

---

## Arquivos principais

### `./_core-pattern.md`
Define o padrão fundamental: `entity_detail_property_unit`

**Quando usar:** Entender base de todas as regras

---

### Regras (10 arquivos)

| Arquivo | Severidade | Auto-fix | Descrição |
|---------|-----------|----------|-----------|
| rule-01-format.md | HIGH | SIM | Formato (snake_case, lowercase, sem acentos) |
| rule-02-consistency.md | CRITICAL | NÃO | Consistência semântica |
| rule-03-units.md | HIGH | NÃO | Unidades obrigatórias |
| rule-04-abbreviations.md | HIGH | SIM | Abreviações permitidas |
| rule-05-no-types.md | MEDIUM | SIM | Sem tipos em nomes |
| rule-06-booleans.md | MEDIUM | CONDICIONAL | Padrão is_/has_ |
| rule-07-dates.md | HIGH | CONDICIONAL | Padrão _date/_at |
| rule-08-foreign-keys.md | CRITICAL | NÃO | Padrão <entity>_id |
| rule-09-composition-order.md | MEDIUM | SIM | Ordem de componentes |
| rule-10-avoid-generic.md | LOW | NÃO | Sem nomes genéricos |

---

### Referências

#### `./reference-units.md`
Tabela de unidades válidas por conceito (peso, volume, temperatura, moeda, etc.)

#### `./reference-severity.md`
Tabela de severidade e ações por tipo de violação

---

## Responsabilidade desta pasta

`naming/` MUST definir convenções de nomenclatura.

`naming/` MUST NOT absorver regras arquiteturais, de implementação ou de qualidade.

---

## Limites

Este README é o roteador compacto do conjunto de naming.

Este README não substitui:

- `./_core-pattern.md`
- regras específicas `./rule-01-format.md` a `./rule-10-avoid-generic.md`
- `./reference-units.md`
- `./reference-severity.md`

---

## Fronteiras

### Pode conter
- convenções de naming
- padrões de nomenclatura
- regras de formato
- regras de semântica
- exemplos válidos e inválidos
- severidade de violações
- tabelas de referência

### Não pode conter
- governança estrutural
- política de naming
- procedimentos de validação
- procedimentos de detecção
- procedimentos de auto-fix
- prompts de enforcement

---

## Relação com os demais diretórios

- é governado por `../../governance/composition/semantic-naming-governance.md`
- é validado por `../../skills/review/semantic-naming-validation.md`
- é detectado por `../../skills/review/semantic-naming-detection.md`
- é corrigido por `../../skills/review/semantic-naming-autofix.md`
- é enforçado por `../../prompts/review/enforce-semantic-naming.md`
- é validado por `../../prompts/hooks/validate-semantic-naming-conformance.md`

---

## Ordem de leitura recomendada

1. **Começar por:** `./_core-pattern.md` (entender base)
2. **Depois:** `./rule-01-format.md` (formato obrigatório)
3. **Depois:** `./rule-02-consistency.md` (consistência crítica)
4. **Depois:** Outras regras conforme necessidade
5. **Referência:** `./reference-units.md` e `./reference-severity.md`

---

## Uso pelo agente

Ao consumir `naming/`, o agente deve:

- começar por `./_core-pattern.md`
- carregar apenas regras necessárias
- tratar normas como restrições obrigatórias
- distinguir obrigação de recomendação
- respeitar severidade de violações
- usar tabelas de referência para validação

---

## Composição das regras

As regras de naming estão decompostas em:

- 1 arquivo de padrão core
- 10 arquivos de regras individuais
- 2 arquivos de referência

Essa decomposição preserva responsabilidade única e permite que o agente carregue apenas o necessário para a tarefa.
