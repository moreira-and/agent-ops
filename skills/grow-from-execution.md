# grow-from-execution

## Tipo do artefato

skill

## Status de injeção

condicional

## Finalidade

Definir o procedimento reutilizável para destilar conhecimento de um `.md` de execução e convertê-lo em artefatos de contexto.

---

## Quando usar

Use esta skill quando precisar:

- analisar execução passada
- identificar padrões reutilizáveis
- separar histórico de conhecimento operacional
- decidir entre criar, atualizar, consolidar ou rejeitar artefatos
- preservar token economy durante crescimento do `agent-ops`

---

## Quando não usar

Não use esta skill como fonte primária para:

- regra obrigatória de qualidade
- perfil executor
- prompt de workflow
- documentação humana

Consulte, respectivamente:

- `../rules/growth-artifact-quality.md`
- `../agents/agentops-growth-architect.md`
- `../prompts/grow-from-execution.md`
- `../docs/`

---

## Dependências relacionadas

- `../MANIFEST.md`
- `../governance/principles/core-principles.md`
- `../governance/composition/context-composition.md`
- `../governance/lifecycle/artifact-lifecycle-policy.md`
- `../governance/authoring/markdown-authoring-standard.md`
- `../governance/quality/artifact-quality-standard.md`
- `../rules/growth-artifact-quality.md`

---

## Precedência

Esta skill deve ser consumida depois do prompt, da governança, do agente e das rules aplicáveis.

---

## Procedimento operacional

### 1. Ler a execução
Ler o `.md` de execução indicado pelo prompt.

Identificar:

- objetivo original
- ações executadas
- decisões tomadas
- lacunas encontradas
- padrões recorrentes
- correções aplicadas

### 2. Separar histórico de conhecimento
Classificar cada trecho como:

- histórico bruto
- evidência de padrão
- decisão recorrente
- procedimento reutilizável
- restrição de qualidade
- candidato a artefato

Histórico bruto MUST NOT ser copiado para artefato injetável.

### 3. Classificar responsabilidade
Aplicar a matriz:

| Critério | Classificação |
|----------|---------------|
| inicia tarefa ou fluxo | prompt |
| define missão, escopo ou limites de executor | agent |
| impõe obrigação, restrição ou guardrail de output | rule |
| descreve técnica, heurística ou procedimento | skill |
| valida checkpoint | hook |
| governa estrutura, autoria, lifecycle ou composição | governance |
| explica contexto humano ou histórico | docs ou rejeição |

### 4. Verificar recorrência
Antes de propor artefato, verificar se o conhecimento:

- pode ocorrer novamente
- melhora seleção ou execução
- reduz ambiguidade
- não depende de circunstância única
- é genérico para qualquer modelo de IA

### 5. Verificar duplicação
Buscar artefato equivalente em:

- `../prompts/`
- `../agents/`
- `../rules/`
- `../skills/`
- `../prompts/hooks/`
- `../governance/`

Se fonte primária existir, preferir atualização incremental ou referência por caminho.

### 6. Decidir ação
Escolher uma ação:

- criar novo artefato
- atualizar artefato existente
- consolidar com fonte primária
- mover proposta para `../docs/`
- rejeitar

### 7. Preservar token economy
O artefato resultante SHOULD:

- ser curto o suficiente para seleção modular
- evitar exemplos redundantes
- referenciar fontes primárias
- não aumentar contexto obrigatório por padrão
- ser compreensível por modelos simples

### 8. Validar antes de concluir
Validar a proposta com:

- `../rules/growth-artifact-quality.md`
- `../prompts/hooks/validate-growth-proposal.md`

---

## Critérios para criar novo arquivo

Crie novo arquivo apenas quando:

- houver responsabilidade única nova
- a recuperação melhorar
- o conhecimento for recorrente
- não houver fonte primária equivalente
- o artefato puder ser injetado independentemente

---

## Critérios para atualizar arquivo existente

Atualize arquivo existente quando:

- a fonte primária já existir
- a mudança for incremental
- a alteração reduzir ambiguidade
- a alteração não quebrar o contrato do arquivo

---

## Critérios para rejeitar

Rejeite quando:

- o conteúdo for histórico bruto
- a evidência for insuficiente
- a decisão for pontual
- a proposta duplicar artefato existente
- a mudança piorar token economy
- a classificação exigir comportamento excepcional demais

---

## Saída esperada

A aplicação desta skill SHOULD produzir:

- conhecimento reutilizável identificado
- conhecimento rejeitado
- classificação por tipo de artefato
- decisão criar, atualizar, consolidar ou rejeitar
- justificativa por decisão
- riscos e validação final

---

## Limites

Esta skill define o procedimento de destilação e classificação.

Esta skill não substitui:

- rule obrigatória de qualidade
- prompt de entrada
- agente executor
- hook de validação
