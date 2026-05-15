# artifact-quality-standard

## Tipo do artefato

governance

## Finalidade

Definir os critérios de qualidade mínimos para arquivos `.md` do `agent-ops`.

---

## Quando usar

Use este arquivo quando precisar:

- revisar um artefato novo
- validar se um arquivo está pronto para uso
- verificar aderência à estrutura do repositório
- avaliar risco de ambiguidade ou alucinação

---

## Quando não usar

Não use este arquivo como fonte primária para:

- qualidade técnica de output
- composição de contexto
- padrão de autoria detalhado
- lifecycle de artefatos

Consulte, respectivamente:

- `../../rules/quality/quality-rules.md`
- `../composition/context-composition.md`
- `../authoring/markdown-authoring-standard.md`
- `../lifecycle/artifact-lifecycle-policy.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../principles/core-principles.md`
- `../authoring/markdown-authoring-standard.md`

---

## Critérios mínimos de qualidade

### 1. Responsabilidade única
O artefato MUST ter responsabilidade principal clara.

### 2. Classificação clara
O artefato SHOULD ser claramente classificável como:

- governance
- agent
- rule
- skill
- prompt
- discovery
- hook prompt

### 3. Propósito explícito
O artefato MUST deixar claro para que serve.

### 4. Escopo explícito
O artefato SHOULD deixar claro o que cobre e o que não cobre.

### 5. Rastreabilidade
Dependências e referências SHOULD ser rastreáveis por caminho.

### 6. Não duplicação
O artefato MUST NOT competir com a fonte primária de outro artefato.

### 7. Utilidade de injeção
O artefato SHOULD justificar sua existência pela utilidade em descoberta, seleção ou injeção.

### 8. Legibilidade
O artefato SHOULD ser legível para humanos e agentes.

### 9. Baixa ambiguidade
O artefato SHOULD minimizar termos vagos e instruções implícitas.

### 10. Aderência estrutural
O artefato MUST respeitar o diretório ao qual pertence.

### 11. Baixo acoplamento
O artefato MUST declarar dependências contextuais relevantes por caminho.

O artefato MUST NOT depender de memória externa, leitura global ou artefato carregado por acaso.

### 12. Alta coesão
O conteúdo do artefato SHOULD servir à mesma responsabilidade principal.

Se o arquivo contiver responsabilidades independentes, ele SHOULD ser dividido.

### 13. Compatibilidade com injeção seletiva
O artefato SHOULD poder ser selecionado e injetado de forma independente quando sua responsabilidade for relevante.

O artefato SHOULD NOT exigir carregamento de contexto não relacionado para ser compreendido.

---

## Sinais de baixa qualidade

Um artefato SHOULD ser revisado se:

- mistura múltiplas responsabilidades
- não deixa claro quando usar
- não deixa claro seus limites
- duplica conteúdo existente
- está no diretório errado
- exige inferência excessiva
- adiciona ruído sem melhorar recuperação ou injeção
- depende de contexto não declarado
- mistura prompt, agent, rule, skill, hook, governance ou documentação humana
- obriga carregamento de artefatos não relacionados

---

## Critério de prontidão

Um artefato está pronto para uso quando:

- tem propósito claro
- tem escopo coerente
- respeita sua categoria
- referencia dependências por caminho, quando necessário
- não duplica fonte primária
- é utilizável por humano e agente com baixa ambiguidade
- preserva baixo acoplamento e alta coesão
- é compatível com composição seletiva

---

## Limites

Este arquivo define padrão de qualidade.

Este arquivo não substitui:

- princípios fundacionais
- composição
- autoria
- lifecycle
