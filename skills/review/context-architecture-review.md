# context-architecture-review

## Tipo do artefato

skill

## Finalidade

Definir procedimento reutilizavel para auditar arquitetura informacional, redundancia, custo de contexto e separacao de responsabilidades.

Esta skill operacionaliza Context Debt Audit sem transformar toda mudanca pequena em processo pesado.

---

## Quando usar

Use esta skill quando:

- `../../prompts/hooks/validate-context-debt.md` for acionado
- houver suspeita de artefatos redundantes ou extensos
- uma feature nova tiver criado muitos arquivos
- um diretorio parecer mal organizado
- for necessario decidir entre manter, cortar, fundir, mover, dividir ou depreciar

---

## Quando nao usar

Nao use esta skill quando:

- a mudanca for local e trivial
- a tarefa for revisao tecnica de codigo ou solucao de dados
- a questao for apenas autoria Markdown
- a decisao exigir primeiro intake, safety ou delegation governance

Consulte, respectivamente:

- `./technical-review.md`
- `../../governance/authoring/markdown-authoring-standard.md`
- `../../prompts/hooks/validate-user-intent.md`
- `../../prompts/hooks/size-task-for-delegation.md`

---

## Dependencias relacionadas

- `../../governance/quality/context-economy-and-responsibility.md`
- `../../prompts/hooks/validate-context-debt.md`
- `../../governance/lifecycle/artifact-synchronization-policy.md`

---

## Procedimento

### 1. Delimitar escopo

Declare quais artefatos, diretorios ou mudancas estao em avaliacao.

Nao audite o repositorio inteiro por reflexo.

### 2. Identificar fonte primaria

Para cada item avaliado, identifique a fonte primaria aplicavel:

- `../../MANIFEST.md`
- `../../governance/`
- README local
- artefato especializado

### 3. Avaliar valor

Pergunte:

```txt
Este artefato melhora selecao, seguranca, manutencao, validacao ou execucao recorrente?
```

Se nao houver valor claro, recomende `MERGE`, `MOVE` ou `DEPRECATE`.

### 4. Avaliar responsabilidade

Verifique se o item mistura:

- governance
- rule
- skill
- prompt
- hook
- docs
- eval
- memory

Mistura sem necessidade indica `SPLIT`, `MOVE` ou `TRIM`.

### 5. Avaliar local

Compare a funcao real com o diretorio atual.

Local errado indica `MOVE`.

### 6. Avaliar redundancia

Identifique se a repeticao e:

- resumo de roteamento aceitavel
- duplicidade normativa inaceitavel

Duplicidade normativa indica `MERGE` ou `TRIM`.

### 7. Avaliar custo

Classifique custo como:

| Custo | Criterio |
|---|---|
| `low` | curto, acionavel e sob demanda |
| `medium` | util, mas exige leitura relevante |
| `high` | longo, redundante ou exige contexto demais |

### 8. Decidir saida

Use uma saida oficial:

- `KEEP`
- `TRIM`
- `MERGE`
- `MOVE`
- `SPLIT`
- `DEPRECATE`

### 9. Declarar sync targets

Quando a recomendacao alterar estrutura, roteador ou contrato, consulte:

- `../../governance/lifecycle/artifact-synchronization-policy.md`
- `../../governance/authoring/artifact-registry.md`

---

## Saida recomendada

```txt
CONTEXT ARCHITECTURE REVIEW
Scope:
Items reviewed:
Findings:
Decisions:
Sync targets:
Residual risk:
Verdict: PASS | CONDITIONAL | FAIL
```

---

## Limites

Esta skill audita e recomenda.

Ela nao remove, move, funde ou divide arquivos sem etapa de implementacao separada e revisada.
