# remediation

## Tipo do artefato

human documentation / remediation tracking

## Finalidade

Este diretorio existe para registrar fluxos humanos de remediacao derivados de auditorias.

Ele transforma achados em fila de execucao com gates, responsaveis sugeridos e criterios de aceite.

---

## Quando usar

Use `remediation/` quando precisar:

- acompanhar remediacoes abertas
- registrar passagem por gates
- preservar evidencia de revisao
- evitar que achados de auditoria virem lista solta

---

## Quando nao usar

Nao use `remediation/` como:

- fonte normativa primaria
- prompt executavel
- rule
- skill
- eval

Consulte, respectivamente:

- `../../MANIFEST.md`
- `../../prompts/`
- `../../rules/`
- `../../skills/`
- `../../evals/`

---

## Arquivos

- `./audit-remediation-orchestration.md`

---

## Limites

Este diretorio registra controle humano de remediacao.

Ele nao altera a precedencia normativa do repositorio e nao entra na composicao padrao.
