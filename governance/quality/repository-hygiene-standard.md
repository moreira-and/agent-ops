# repository-hygiene-standard

## Tipo do artefato

governance

## Finalidade

Definir criterios mecanicos, baratos e objetivos para manter o repositorio limpo.

Regra central:

```txt
Garbage mecanico deve ser bloqueado cedo; julgamento semantico deve escalar.
```

---

## Quando usar

Use este standard quando:

- houver suspeita de arquivo temporario, vazio ou orfao
- uma mudanca criar artefato novo
- uma mudanca criar diretorio novo
- um README, registry ou roteador puder ficar desatualizado
- houver caminho quebrado ou referencia a arquivo removido
- houver candidato a garbage mecanico antes de commit

---

## Quando nao usar

Nao use este standard para:

- decidir valor semantico de artefato
- apagar legado
- fundir, mover ou dividir por criterio conceitual
- substituir Context Debt Audit
- substituir Artifact Lifecycle
- substituir Artifact Synchronization

Consulte, respectivamente:

- `./context-economy-and-responsibility.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../lifecycle/artifact-synchronization-policy.md`
- `../../prompts/hooks/validate-repository-hygiene.md`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `./artifact-quality-standard.md`
- `../lifecycle/artifact-synchronization-policy.md`
- `../../docs/remediation/hygiene-governance-spec.md`

---

## Bloqueios mecanicos

Hygiene Gate MAY bloquear:

- arquivo vazio sem justificativa
- diretorio vazio sem README ou spec
- arquivo temporario de editor
- arquivo binario inesperado
- artefato Markdown novo sem `Tipo do artefato`
- artefato Markdown novo sem `Finalidade`
- spec em `../../docs/remediation/` sem registro em `../../docs/remediation/README.md`
- resultado de eval sem registro em `../../evals/README.md`
- hook novo sem registro em `../../prompts/hooks/README.md`
- rule nova sem registro no README local
- skill nova sem registro no README local
- caminho quebrado em README, INDEX, MANIFEST, registry ou composition
- marcador de conflito de merge

---

## Escalacoes obrigatorias

Hygiene Gate MUST escalate quando:

- a decisao depender de valor semantico
- o arquivo parecer legado substituido
- houver proposta de remocao
- houver duvida entre `MERGE`, `MOVE`, `SPLIT` ou `DEPRECATE`
- o impacto exigir sync targets

Use:

- `ESCALATE_CONTEXT_DEBT` para julgamento de valor, redundancia ou local correto
- `ESCALATE_LIFECYCLE` para legado, depreciacao ou remocao

---

## Legado

Legado MUST NOT ser tratado como garbage automaticamente.

Antes de remover legado, deve existir:

- evidencia;
- substituto;
- nota de migracao;
- condicao de remocao;
- aprovacao ou decisao do orquestrador.

---

## Saidas oficiais

- `PASS`
- `FAIL_GARBAGE`
- `FAIL_BROKEN_REFERENCE`
- `FAIL_MISSING_REGISTRATION`
- `ESCALATE_CONTEXT_DEBT`
- `ESCALATE_LIFECYCLE`

---

## Criterio de conformidade

Uma verificacao de higiene esta conforme quando:

- bloqueia apenas problemas mecanicos;
- cita arquivo ou referencia com evidencia;
- nao apaga arquivo automaticamente;
- nao decide valor semantico;
- escala legado para lifecycle;
- escala redundancia ou valor para Context Debt Audit.

---

## Limites

Este standard governa higiene mecanica.

Ele nao substitui:

- `../../MANIFEST.md`
- `./context-economy-and-responsibility.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../lifecycle/artifact-synchronization-policy.md`
