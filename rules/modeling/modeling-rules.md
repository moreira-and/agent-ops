# modeling-rules

## Tipo do artefato

rule

## Finalidade

Definir normas para modelagem de dados e estruturas relacionadas no contexto de engenharia de dados.

---

## Quando usar

Use este arquivo quando precisar:

- definir estruturas de dados
- desenhar contratos
- revisar coerência de modelagem
- orientar granularidade e consistência semântica

---

## Quando não usar

Não use este arquivo como fonte primária para:

- arquitetura geral
- implementação
- naming detalhado
- skill de modelagem

Consulte, respectivamente:

- `../architecture/architecture-rules.md`
- `../coding/coding-rules.md`
- `../naming/README.md`
- `../../skills/modeling/data-modeling.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../architecture/architecture-rules.md`

---

## Normas

### 1. Modelagem orientada ao domínio
A modelagem MUST refletir o domínio e o uso esperado dos dados.

### 2. Entidades com significado claro
Estruturas modeladas MUST possuir semântica clara e nomes compreensíveis.

### 3. Granularidade consistente
A granularidade SHOULD ser consistente com o objetivo analítico, operacional ou contratual do artefato.

### 4. Evitar ambiguidade estrutural
Campos, entidades e contratos MUST evitar interpretações concorrentes.

### 5. Evolução controlada
A modelagem SHOULD permitir evolução sem quebrar desnecessariamente consumidores previsíveis.

### 6. Contratos explícitos
Quando aplicável, contratos de dados SHOULD explicitar entradas, saídas, formato e restrições relevantes.

### 7. Coerência entre estrutura e uso
A forma modelada SHOULD servir ao consumo real esperado, e SHOULD NOT existir apenas por conveniência técnica local.

---

## Limites

Este arquivo define normas gerais de modelagem.

Este arquivo não substitui:

- normas arquiteturais
- convenções de naming
- critérios de qualidade
- regras de implementação
