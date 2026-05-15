# semantic-naming-governance

## Tipo do artefato

governance

## Finalidade

Definir os princípios de governança para naming semântico em ambientes de engenharia de dados.

Este arquivo é a fonte primária para política de nomenclatura como infraestrutura semântica.

---

## Quando usar

Use este arquivo quando precisar:

- entender por que naming é governança
- decidir se uma convenção de naming deve ser criada
- validar se uma regra de naming está no escopo correto
- orientar evolução de padrões de nomenclatura
- arbitrar conflitos entre conveniência local e consistência global

---

## Quando não usar

Não use este arquivo como fonte primária para:

- regras específicas de naming
- procedimentos de validação
- detecção de violações
- correção automática
- prompts de enforcement

Consulte, respectivamente:

- `../../rules/naming/README.md`
- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`
- `../../prompts/review/enforce-semantic-naming.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../principles/core-principles.md`
- `../../rules/naming/README.md`

---

## Princípios de governança

### 1. Naming é infraestrutura semântica

Convenções de naming não são estéticas.

Naming é infraestrutura que:

- reduz ambiguidade
- melhora discoverabilidade
- facilita lineage
- habilita raciocínio automatizado
- escala manutenção

---

### 2. Consistência > preferência local

Consistência global é mais importante que conveniência local.

Razão:

- um desenvolvedor economiza 10 segundos
- 100 desenvolvedores perdem 1 minuto cada
- custo total: 100 minutos de confusão

---

### 3. Determinismo obrigatório

Mesmo conceito semântico = sempre mesmo nome.

Não permitir:

- customer_id e id_customer
- weight e peso
- amount_brl e vlr_total

---

### 4. Semântica explícita

Nomes devem comunicar significado, não implementação.

Não permitir:

- customer_id_int (tipo pertence ao schema)
- weight_float (tipo pertence ao schema)
- temp_var (semântica vaga)

---

### 5. Unidades são mandatórias

Valores mensuráveis devem declarar unidades explicitamente.

Não permitir:

- weight (qual unidade?)
- temperature (Celsius? Fahrenheit?)
- distance (metros? quilômetros?)

Exigir:

- weight_kg
- temperature_celsius
- distance_m

---

### 6. Enforcement é multi-camada

Naming governance opera em 4 camadas:

1. **Política** (este arquivo) - por que importa
2. **Regras** (rules/naming/) - o que é permitido
3. **Detecção** (skills/review/) - como encontrar violações
4. **Enforcement** (prompts/review/) - como corrigir

Cada camada tem responsabilidade única.

---

### 7. Risco de rename deve ser explícito

Renomeações podem quebrar:

- contratos externos
- linhagem de dados
- queries em produção
- documentação

Portanto:

- auto-fix é permitido para casos óbvios
- human review é obrigatório para casos ambíguos
- racional técnico deve ser documentado

---

### 8. Ambiguidade bloqueia auto-fix

Se múltiplas interpretações semânticas forem possíveis:

- não renomear automaticamente
- sinalizar para revisão humana
- explicar o risco
- sugerir alternativas

---

## Limites

Este arquivo define política de naming como governança.

Este arquivo não substitui:

- regras específicas de naming
- procedimentos de validação
- prompts de enforcement
- padrões de qualidade geral

---

## Relação com demais artefatos

- governa `../../rules/naming/`
- governa `../../skills/review/semantic-naming-validation.md`
- governa `../../skills/review/semantic-naming-detection.md`
- governa `../../skills/review/semantic-naming-autofix.md`
- governa `../../prompts/review/enforce-semantic-naming.md`
- obedece `../principles/core-principles.md`
- obedece `../../MANIFEST.md`

---

## Comportamento esperado do agente

Ao consumir este arquivo, o agente deve:

- tratar naming como infraestrutura crítica
- priorizar consistência sobre conveniência
- respeitar limites de auto-fix
- exigir racional técnico para renomeações
- sinalizar ambiguidade antes de agir
