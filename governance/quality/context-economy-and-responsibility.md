# context-economy-and-responsibility

## Tipo do artefato

governance

## Finalidade

Definir criterios para conter divida de arquitetura informacional, custo cognitivo e crescimento sem valor operacional.

Regra central:

```txt
Todo artefato deve provar valor, responsabilidade unica, local correto e custo justificavel.
```

---

## Quando usar

Use este standard quando:

- um artefato parecer redundante, longo ou caro
- uma mudanca criar varios arquivos novos
- houver duvida sobre local correto de um arquivo
- um diretorio crescer sem fronteira clara
- README, registry, eval, rule, skill, hook ou governance parecerem sobrepostos
- uma auditoria de Context Debt Audit for solicitada

---

## Quando nao usar

Nao use este standard quando:

- a mudanca for typo local
- o criterio de aceite for pequeno e local
- a revisao de qualidade geral em `./artifact-quality-standard.md` for suficiente
- a pergunta for sobre qualidade tecnica de uma solucao de dados

Consulte, respectivamente:

- `./artifact-quality-standard.md`
- `../../rules/quality/quality-rules.md`
- `../../prompts/hooks/validate-context-debt.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `./artifact-quality-standard.md`
- `../composition/context-composition.md`
- `../../docs/remediation/context-debt-audit-spec.md`

---

## Criterios

### 1. Valor operacional

O artefato MUST provar pelo menos um valor real:

- melhora selecao de contexto
- reduz ambiguidade
- reduz risco operacional
- evita duplicidade
- melhora manutencao
- melhora validacao
- orienta execucao recorrente

Artefato sem valor comprovavel SHOULD ser removido, fundido ou movido.

### 2. Responsabilidade unica

O artefato SHOULD ter uma responsabilidade principal clara.

O artefato SHOULD NOT misturar norma, procedimento, exemplo, registro historico e validacao no mesmo corpo.

### 3. Local correto

O artefato MUST estar no diretorio que melhor representa sua funcao:

| Funcao | Local esperado |
|---|---|
| norma estrutural | `../../governance/` |
| restricao de output ou entrada humana | `../../rules/` |
| capacidade operacional | `../../skills/` |
| ponto de entrada ou checkpoint | `../../prompts/` |
| explicacao humana | `../../docs/` |
| validacao de comportamento | `../../evals/` |
| memoria auxiliar | `../../_memory/` |

### 4. Redundancia

Duplicidade aceitavel MUST ser curta e servir discovery.

Duplicidade inaceitavel ocorre quando:

- a mesma regra completa aparece em mais de um arquivo
- README copia spec
- prompt embute governance
- skill vira norma obrigatoria
- eval explica regra em vez de validar comportamento

### 5. Custo cognitivo

O artefato SHOULD ser pequeno o bastante para decisao operacional.

Sinais de custo injustificado:

- listas longas sem decisao
- exemplos extensos em artefato operacional
- linguagem abstrata sem acao
- dependencias demais para tarefa comum
- repeticao de contrato ja definido em fonte primaria

### 6. Custo de contexto

Artefato auxiliar, humano, historico ou de validacao MUST NOT entrar na composicao padrao.

Artefato extenso SHOULD ser resumido em roteador e carregado sob demanda.

### 7. Governanca real

Regra declarada SHOULD ter caminho de enforcement ou validacao:

- composition
- hook
- rule
- skill
- eval
- sync target

Governanca sem enforcement ou criterio de aceite SHOULD ser rebaixada para documentacao humana ou removida.

---

## Saidas oficiais

Uma auditoria de contexto MUST usar uma destas saidas:

- `KEEP`
- `TRIM`
- `MERGE`
- `MOVE`
- `SPLIT`
- `DEPRECATE`

---

## Criterio de conformidade

Uma decisao esta conforme quando:

- cita evidencia por caminho
- declara custo e valor
- diferencia redundancia aceitavel de inaceitavel
- preserva fonte primaria
- evita criar novo artefato sem autonomia semantica
- nao transforma auditoria em fluxo obrigatorio para mudanca pequena

---

## Limites

Este standard governa economia de contexto e responsabilidade de artefatos.

Ele nao substitui:

- `../../MANIFEST.md`
- `./artifact-quality-standard.md`
- `../composition/context-composition.md`
- `../lifecycle/artifact-synchronization-policy.md`
