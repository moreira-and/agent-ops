# enforce-semantic-naming

## Tipo do artefato

prompt

## Finalidade

Definir o ponto de entrada para enforcement de naming semantico em schemas, SQL models, DataFrames, aliases e transformacoes de dados.

Este prompt e um orquestrador. Ele nao define regra primaria, matriz de severidade, catalogo de unidades nem tutorial de auto-fix.

---

## Quando usar

Use este prompt quando precisar:

- validar nomes contra o conjunto `rules/naming/`
- detectar violacoes semanticas de naming
- separar auto-fix seguro de revisao humana
- gerar relatorio auditavel de naming
- preparar uma revisao antes de merge, deploy ou conclusao de tarefa

---

## Quando nao usar

Nao use este prompt para:

- desenhar arquitetura de dados
- implementar transformacao de dados
- decidir significado de negocio ausente
- carregar exemplos humanos como contexto padrao

Consulte, conforme o caso:

- `../../agents/data-architecture/solid-data-architect.md`
- `../../agents/data-engineering/solid-data-engineer.md`
- `../../docs/examples/semantic-naming-examples.md` apenas quando o usuario pedir exemplo humano

---

## Composicao recomendada

### Base

- `../../MANIFEST.md`
- `../../governance/principles/core-principles.md`
- `../../governance/composition/context-composition.md`

### Naming

- `../../governance/composition/semantic-naming-governance.md`
- `../../agents/data-engineering/semantic-naming-enforcement-agent.md`
- `../../rules/naming/README.md`
- `../../rules/naming/_core-pattern.md`
- regras especificas selecionadas por `../../rules/naming/README.md`
- `../../rules/naming/reference-severity.md`
- `../../rules/naming/reference-units.md` quando houver valores mensuraveis

### Skills

- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`

---

## Entradas obrigatorias

O agente MUST receber ou solicitar:

- `artifact`: schema, SQL, DataFrame schema, codigo ou lista de nomes
- `scope`: quais nomes validar
- `semantic_context`: dominio, entidades, relacionamentos e contratos conhecidos
- `constraints`: restricoes de compatibilidade, contratos externos, linagem ou migracao

Se `semantic_context` ou `constraints` forem insuficientes para uma decisao segura, o agente MUST retornar `CONDITIONAL` ou solicitar esclarecimento. Nao invente significado.

---

## Instrucao operacional

Ao executar este prompt, o agente MUST:

1. Carregar o roteador `../../rules/naming/README.md`.
2. Selecionar somente as regras aplicaveis ao escopo.
3. Usar `../../rules/naming/reference-severity.md` como unica fonte primaria de severidade.
4. Usar `../../rules/naming/reference-units.md` como unica fonte primaria de unidades validas.
5. Detectar violacoes com `../../skills/review/semantic-naming-detection.md`.
6. Validar conformidade com `../../skills/review/semantic-naming-validation.md`.
7. Decidir auto-fix com `../../skills/review/semantic-naming-autofix.md`.
8. Separar cada achado em `AUTO_FIXABLE`, `REQUIRES_REVIEW` ou `BLOCKED`.
9. Documentar evidencia, impacto e acao para cada achado.

---

## Regras de decisao

- Violacao `CRITICAL` MUST bloquear merge/conclusao ate resolucao ou decisao humana explicita.
- Violacao `HIGH` nao bloqueia automaticamente, mas MUST ter racional e acao documentados.
- Ambiguidade de unidade, entidade, tipo ou contrato externo MUST impedir auto-fix silencioso.
- Rename que pode quebrar query, API, linagem, contrato externo ou documentacao operacional MUST ser `BLOCKED`.
- Auto-fix so e permitido quando a transformacao for deterministica, local e de baixo risco.

---

## Saida esperada

O agente MUST produzir saida estruturada com estes campos:

```txt
semantic_naming_enforcement
status: PASS | FAIL | CONDITIONAL
scope:
artifacts_reviewed:
rules_loaded:
summary:
  total_names:
  violations:
  critical:
  high:
  medium:
  low:
findings:
  - name:
    rule:
    severity:
    evidence:
    impact:
    recommendation:
    action: AUTO_FIXABLE | REQUIRES_REVIEW | BLOCKED
    rationale:
pending_questions:
final_recommendation: APPROVE | BLOCK | REQUIRES_REVIEW
```

---

## Checkpoints

Antes de concluir, validar:

- [ ] O contexto carregado foi minimo e rastreavel?
- [ ] Cada regra aplicada foi selecionada por necessidade?
- [ ] Severidade veio de `reference-severity.md`?
- [ ] Unidades vieram de `reference-units.md`?
- [ ] Casos ambiguos nao receberam auto-fix?
- [ ] Contratos externos foram preservados?
- [ ] Cada achado tem evidencia, impacto e recomendacao?

---

## Exemplos e regressao

Exemplos completos ficam fora do contexto padrao:

- `../../docs/examples/semantic-naming-examples.md`

Casos minimos de regressao:

- `../../evals/manual-regression-suite.md` (`EVAL-004`, `EVAL-005`, `EVAL-006`)

---

## Limites

Este prompt nao substitui:

- `../../rules/naming/README.md`
- `../../rules/naming/reference-severity.md`
- `../../rules/naming/reference-units.md`
- `../../skills/review/semantic-naming-validation.md`
- `../../skills/review/semantic-naming-detection.md`
- `../../skills/review/semantic-naming-autofix.md`
