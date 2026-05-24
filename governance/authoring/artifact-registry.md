# artifact-registry

Artifact ID: governance.artifact-registry
Kind: governance

## Tipo do artefato

governance

## Finalidade

Registrar artefatos criticos e auxiliares governados com seus sync targets.

Este registry ajuda a decidir quais arquivos revisar quando um artefato muda, sem colocar metadata completo em todos os arquivos.

---

## Quando usar

Use este registry quando:

- alterar artefato central, auxiliar ou critico
- precisar saber quais roteadores podem ficar desatualizados
- revisar `_memory/`, futura `_extensions/` ou futura `_distillation/`
- preparar mudanca de contrato, composicao, readiness ou eval

---

## Quando nao usar

Nao use este registry como:

- fonte normativa primaria
- catalogo de todos os arquivos
- substituto de README local
- substituto de `../../MANIFEST.md`

Consulte, respectivamente:

- `../../MANIFEST.md`
- `./markdown-authoring-standard.md`
- `../lifecycle/artifact-synchronization-policy.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `./markdown-authoring-standard.md`
- `../lifecycle/artifact-synchronization-policy.md`

---

## Registry

| Artifact ID | Path | Kind | Primary source | Status | Review cadence | Last reviewed | Sync targets |
|---|---|---|---|---|---|---|---|
| `root.manifest` | `../../MANIFEST.md` | manifest | self | active | quarterly | 2026-05-24 | `../../README.md`, `../../INDEX.md`, `../../governance/composition/context-composition.md`, `../../evals/manual-regression-suite.md` |
| `root.readme` | `../../README.md` | readme / discovery | `../../MANIFEST.md` | active | quarterly | 2026-05-24 | `../../INDEX.md`, `../../MANIFEST.md`, `../../docs/remediation/audit-remediation-orchestration.md` |
| `root.index` | `../../INDEX.md` | discovery / llm-index | `../../MANIFEST.md` | active | quarterly | 2026-05-24 | `../../README.md`, `../../MANIFEST.md`, `../../governance/composition/context-composition.md`, `../../evals/manual-regression-suite.md` |
| `governance.context-composition` | `../composition/context-composition.md` | governance | `../../MANIFEST.md` | active | quarterly | 2026-05-24 | `../../README.md`, `../../INDEX.md`, `../../evals/manual-regression-suite.md` |
| `governance.artifact-registry` | `./artifact-registry.md` | governance | `../lifecycle/artifact-synchronization-policy.md` | active | quarterly | 2026-05-24 | `./README.md`, `../lifecycle/artifact-synchronization-policy.md`, `../../evals/manual-regression-suite.md` |
| `governance.artifact-lifecycle-policy` | `../lifecycle/artifact-lifecycle-policy.md` | governance | `../../MANIFEST.md` | active | quarterly | 2026-05-24 | `../lifecycle/README.md`, `../lifecycle/artifact-synchronization-policy.md`, `../../evals/manual-regression-suite.md` |
| `governance.artifact-synchronization-policy` | `../lifecycle/artifact-synchronization-policy.md` | governance | `../../docs/remediation/artifact-synchronization-spec.md` | active | quarterly | 2026-05-24 | `./artifact-registry.md`, `../lifecycle/README.md`, `../../evals/manual-regression-suite.md` |
| `memory.root` | `../../_memory/README.md` | governed-memory / discovery | `../../docs/remediation/governed-memory-spec.md` | active | quarterly | 2026-05-24 | `../../README.md`, `../../INDEX.md`, `../../MANIFEST.md`, `../composition/context-composition.md`, `../../evals/manual-regression-suite.md` |
| `memory.project-decisions` | `../../_memory/project-decisions.md` | governed-memory | `../../_memory/README.md` | active | quarterly | 2026-05-24 | `../../_memory/README.md`, `./artifact-registry.md` |
| `memory.stable-preferences` | `../../_memory/stable-preferences.md` | governed-memory | `../../_memory/README.md` | active | quarterly | 2026-05-24 | `../../_memory/README.md`, `./artifact-registry.md` |
| `memory.lessons-learned` | `../../_memory/lessons-learned.md` | governed-memory | `../../_memory/README.md` | active | quarterly | 2026-05-24 | `../../_memory/README.md`, `./artifact-registry.md` |
| `evals.manual-regression-suite` | `../../evals/manual-regression-suite.md` | validation / human-review | `../../evals/README.md` | active | quarterly | 2026-05-24 | `../../evals/README.md`, `../../docs/remediation/audit-remediation-orchestration.md` |
| `docs.artifact-synchronization-spec` | `../../docs/remediation/artifact-synchronization-spec.md` | human documentation / execution spec | `../../MANIFEST.md` | active | none | 2026-05-24 | `./artifact-registry.md`, `../lifecycle/artifact-synchronization-policy.md`, `../../docs/remediation/README.md` |
| `docs.small-model-execution-mode-spec` | `../../docs/remediation/small-model-execution-mode-spec.md` | human documentation / execution spec | `../../MANIFEST.md` | active | none | 2026-05-24 | `../composition/context-composition.md`, `../../INDEX.md`, `../../README.md`, `../../evals/manual-regression-suite.md`, `../../docs/remediation/README.md` |
| `docs.delegation-governance-spec` | `../../docs/remediation/delegation-governance-spec.md` | human documentation / execution spec | `../../MANIFEST.md` | active | none | 2026-05-24 | `../composition/context-composition.md`, `../../INDEX.md`, `../../README.md`, `../../prompts/hooks/README.md`, `../../rules/architecture/README.md`, `../../skills/orchestration/README.md`, `../../evals/manual-regression-suite.md`, `../../docs/remediation/README.md` |

---

## Limites

Este registry lista apenas artefatos criticos, centrais ou auxiliares governados.

Ele nao deve crescer para catalogar todo arquivo do repositorio.

Em caso de conflito, prevalece `../../MANIFEST.md` e a fonte primaria indicada no artefato.
