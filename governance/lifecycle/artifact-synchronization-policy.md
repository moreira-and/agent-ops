# artifact-synchronization-policy

Artifact ID: governance.artifact-synchronization-policy
Kind: governance

## Tipo do artefato

governance

## Finalidade

Definir como classificar impacto de mudancas e escolher quais artefatos precisam ser revisados.

Esta policy evita duas falhas:

- atualizar arquivos demais por reflexo;
- deixar roteadores, contratos ou evals desatualizados.

---

## Quando usar

Use esta policy quando:

- criar, mover, renomear ou remover artefato
- alterar contrato, fluxo, guardrail, precedencia ou composicao
- alterar `README.md`, `INDEX.md`, `MANIFEST.md`, `governance/`, `_memory/` ou evals
- decidir sync targets para um item do registry
- revisar se uma mudanca precisa de eval ou remediacao

---

## Quando nao usar

Nao use esta policy como fonte primaria para:

- padrao de escrita Markdown
- composicao de contexto
- qualidade de output
- regra tecnica especializada

Consulte, respectivamente:

- `../authoring/markdown-authoring-standard.md`
- `../composition/context-composition.md`
- `../quality/artifact-quality-standard.md`
- `../../rules/`

---

## Dependencias relacionadas

- `../../MANIFEST.md`
- `../authoring/artifact-registry.md`
- `../authoring/markdown-authoring-standard.md`
- `./artifact-lifecycle-policy.md`

---

## Metadata minimo inline

Artefatos criticos SHOULD declarar no topo:

```txt
Artifact ID: <namespace.name>
Kind: <kind>
```

Campos adicionais SHOULD ficar no registry, nao no arquivo.

`Reviewed against commit` MAY ser usado apenas em auditoria, release ou artefato critico.

Artefatos simples MAY nao ter metadata inline.

---

## Classes de impacto

| Classe | Quando usar | Acao minima |
|---|---|---|
| `NONE` | Mudanca local sem efeito em roteamento, contrato ou comportamento | Nenhum sync externo |
| `LOCAL` | Muda escopo ou arquivo dentro de um diretorio | Revisar README local |
| `ROUTER` | Muda descoberta, nomes, estrutura ou pontos de entrada | Revisar README local, `../../README.md` e `../../INDEX.md` |
| `CONTRACT` | Muda comportamento, regra, guardrail, composicao ou precedencia | Revisar `../../MANIFEST.md`, `../composition/context-composition.md`, hooks e evals aplicaveis |
| `AUXILIARY` | Muda `_memory/`, futura `_extensions/` ou futura `_distillation/` | Revisar registry, composition, root routers e evals aplicaveis |
| `RELEASE` | Muda readiness, resultado de auditoria ou criterio de versao | Revisar evals, remediation e registros de release |

---

## Regras de sync targets

### README local

Atualize README local quando a mudanca:

- adiciona arquivo ao diretorio;
- remove arquivo do diretorio;
- muda finalidade do diretorio;
- muda arquivo primario ou lista de arquivos.

### Root README

Atualize `../../README.md` quando a mudanca:

- altera estrutura raiz;
- altera dominio de uma area;
- altera workflow principal;
- altera status de uso;
- adiciona diretorio auxiliar governado.

### INDEX

Atualize `../../INDEX.md` quando a mudanca:

- cria novo ponto de partida para LLM;
- altera roteador barato;
- adiciona diretorio auxiliar que pode ser descoberto sob demanda;
- altera o que fica fora da composicao padrao.

### MANIFEST

Atualize `../../MANIFEST.md` quando a mudanca:

- altera taxonomia oficial;
- altera estrutura raiz;
- altera precedencia;
- altera modelo operacional;
- promove uma policy para contrato oficial.

### Governance de composicao

Atualize `../composition/context-composition.md` quando a mudanca:

- altera `intake -> find -> select -> inject -> execute`;
- altera regra de selecao;
- altera contexto padrao;
- adiciona fonte auxiliar candidata em `find`.

### Evals

Atualize `../../evals/manual-regression-suite.md` quando a mudanca:

- altera comportamento esperado;
- adiciona guardrail;
- adiciona diretorio auxiliar;
- altera formato de saida ou checkpoint;
- corrige falha que deve virar regressao.

### Remediation

Atualize `../../docs/remediation/audit-remediation-orchestration.md` quando a mudanca:

- implementa spec;
- fecha achado de auditoria;
- altera readiness ou status de release;
- exige rastreabilidade de gates.

---

## Diretorios auxiliares

Diretorios prefixados com `_` sao auxiliares e MUST NOT entrar na composicao padrao.

### `_memory/`

Impact class padrao: `AUXILIARY`.

Sync targets usuais:

- `../../README.md`
- `../../INDEX.md`
- `../../MANIFEST.md`
- `../composition/context-composition.md`
- `../../evals/manual-regression-suite.md`
- `../authoring/artifact-registry.md`

### `_extensions/`

Impact class padrao: `AUXILIARY`.

Antes de criar, deve existir spec propria.

Sync targets usuais:

- `../../README.md`
- `../../INDEX.md`
- `../../MANIFEST.md`
- `../composition/context-composition.md`
- `../../evals/`
- `../authoring/artifact-registry.md`

### `_distillation/`

Impact class padrao: `AUXILIARY`.

Antes de criar, deve existir policy especifica de dados e schema.

`_distillation/` MUST NOT conter chain-of-thought bruto, segredo, dado pessoal ou dado de cliente sem politica explicita.

Sync targets usuais:

- `../../README.md`
- `../../INDEX.md`
- `../../MANIFEST.md`
- `../../evals/README.md`
- `../authoring/artifact-registry.md`

---

## Procedimento minimo

Para qualquer mudanca relevante:

1. Classificar impacto.
2. Consultar `../authoring/artifact-registry.md`.
3. Revisar sync targets aplicaveis.
4. Atualizar README local quando houver arquivo novo ou removido.
5. Atualizar eval quando o comportamento esperado mudar.
6. Registrar remediacao quando a mudanca implementar spec ou fechar achado.

---

## Criterio de conformidade

Uma mudanca esta sincronizada quando:

- tem classe de impacto coerente;
- sync targets relevantes foram revisados;
- roteadores alterados refletem a estrutura real;
- registry foi atualizado quando artefato critico mudou;
- eval cobre mudanca comportamental;
- nao houve metadata pesado em folhas simples.

---

## Limites

Esta policy governa sincronizacao de artefatos.

Ela nao substitui:

- `../../MANIFEST.md`
- `../authoring/markdown-authoring-standard.md`
- `./artifact-lifecycle-policy.md`
- `../composition/context-composition.md`
- `../../evals/`
