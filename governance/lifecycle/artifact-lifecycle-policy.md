# artifact-lifecycle-policy

Artifact ID: governance.artifact-lifecycle-policy
Kind: governance

## Tipo do artefato

governance

## Finalidade

Definir quando artefatos do `agent-ops` devem ser criados, divididos, consolidados, movidos ou removidos.

---

## Quando usar

Use este arquivo quando precisar:

- decidir se um novo artefato deve ser criado
- dividir um arquivo existente
- consolidar conteúdos sobrepostos
- remover artefatos obsoletos
- controlar crescimento estrutural

---

## Quando não usar

Não use este arquivo como fonte primária para:

- composição de contexto
- padrão de autoria
- checklist de qualidade
- regra técnica de output

Consulte, respectivamente:

- `../composition/context-composition.md`
- `../authoring/markdown-authoring-standard.md`
- `../quality/artifact-quality-standard.md`
- `../../rules/`

---

## Dependências relacionadas

- `../../MANIFEST.md`
- `../principles/core-principles.md`
- `../quality/artifact-quality-standard.md`

---

## Regras de criação

Um novo artefato SHOULD ser criado quando:

- houver responsabilidade nova e clara
- houver reutilização em múltiplos contextos
- a separação melhorar recuperação ou governança
- a separação reduzir ambiguidade
- o novo conhecimento puder ser plugado sem quebrar contratos existentes

Um novo artefato SHOULD NOT ser criado quando:

- a diferença for apenas cosmética
- não houver autonomia semântica
- a separação gerar fragmentação sem ganho real
- exigir mudança global para acomodar um caso específico

---

## Regras de divisão

Um artefato SHOULD ser dividido quando:

- concentrar múltiplas responsabilidades centrais
- misturar norma e execução
- misturar identidade e capacidade
- misturar descoberta e conteúdo primário
- passar a ser reutilizado parcialmente em múltiplos fluxos
- obrigar agentes a carregar contexto que não precisam

---

## Regras de consolidação

Artefatos SHOULD ser consolidados quando:

- a separação não trouxer ganho real
- houver microfragmentação
- a navegação se tornar artificialmente complexa
- múltiplos arquivos dependerem sempre do mesmo bloco pequeno e inseparável

---

## Regras de extração de fonte primária

Quando conteúdo equivalente surgir em múltiplos arquivos:

- uma fonte primária MUST ser definida
- o conteúdo compartilhado MUST ser extraído
- os demais arquivos MUST passar a referenciá-la por caminho

---

## Regras de extensão plugável

A evolução do `agent-ops` MUST preservar o padrão `intake -> find -> select -> inject -> execute`.

Ao adicionar novo conhecimento:

- prefira artefato especializado
- preserve contratos existentes
- declare dependências por caminho
- mantenha baixo acoplamento
- evite reescrever arquivos centrais sem necessidade

A capacidade de crescimento só é válida quando novos artefatos podem ser selecionados e injetados de forma independente.

Mudancas relevantes SHOULD classificar impacto conforme `./artifact-synchronization-policy.md`.

### Critério para `grow`

A capacidade `grow` MUST evoluir o `agent-ops` como sistema modular de contexto.

Ela MUST:

- criar ou atualizar artefatos plugáveis
- preservar contratos existentes
- evitar regras embutidas em prompts
- evitar skills embutidas em agents
- evitar skills como normas obrigatórias
- evitar rules como tutoriais operacionais
- evitar governance como regra de output
- declarar dependências contextuais por caminho

---

## Regras de movimentação

Um artefato SHOULD ser movido quando:

- estiver em diretório semanticamente incorreto
- sua responsabilidade primária mudar
- a nova localização melhorar recuperação, clareza ou governança

---

## Regras de remoção

Um artefato SHOULD ser removido quando:

- estiver obsoleto
- tiver sido substituído por fonte primária mais adequada
- não tiver valor real de recuperação ou injeção
- mantiver duplicação desnecessária

---

## Status de lifecycle

Artefatos podem usar status quando isso reduzir ambiguidade operacional:

- `active`: pronto para uso conforme seu escopo
- `draft`: ainda em construcao ou revisao
- `deprecated`: substituido ou mantido apenas por compatibilidade
- `removed`: removido da composicao e mantido apenas em historico externo, quando existir

### Regra de depreciacao

Um artefato `deprecated` MUST declarar:

- motivo da depreciacao
- caminho do substituto, quando houver
- condicao para remocao

Artefato depreciado MUST NOT ser selecionado por padrao.

### Regra de versao

Mudancas devem preservar compatibilidade semantica sempre que possivel.

Quando uma mudanca alterar contrato de uso, entrada, saida, gate ou precedencia, ela SHOULD registrar a decisao na documentacao humana ou no fluxo de remediacao aplicavel.

---

## Regra de contenção

Toda mudança estrutural SHOULD responder claramente:

- qual problema resolve
- por que não cabe no artefato atual
- qual responsabilidade única preserva
- como evita duplicação

---

## Limites

Este arquivo define lifecycle dos artefatos.

Este arquivo não define:

- padrão de autoria
- composição de contexto
- checklist completo de qualidade
