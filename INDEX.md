# INDEX

Artifact ID: root.index
Kind: discovery / llm-index

## Tipo do artefato

discovery / llm-index

## Finalidade

Roteador barato para descoberta inicial por LLM.

Use este arquivo apenas para encontrar o ponto de partida. Depois selecione o roteador adequado e carregue somente o contexto necessario.

---

## Fonte normativa

- `./MANIFEST.md`

Em caso de conflito, este indice perde para:

1. `./MANIFEST.md`
2. `./governance/`
3. diretorio especializado aplicavel
4. `./README.md`

---

## Ordem de uso

1. Ler este indice somente quando o ponto de partida ainda nao estiver claro.
2. Se o pedido humano estiver vago ou arriscado, iniciar por intake.
3. Escolher um roteador por caminho.
4. Carregar apenas os artefatos necessarios.
5. Descartar este indice quando o contexto especifico estiver escolhido.

---

## Status de injecao

- MAY ser carregado no inicio de discovery quando o roteador ainda nao esta claro.
- MUST ser descartado depois que o contexto especifico for selecionado.
- MUST NOT ser usado como fonte normativa primaria.

---

## Roteadores principais

| Necessidade | Comece por |
|---|---|
| resolver conflito estrutural | `./MANIFEST.md` |
| entender uso humano geral | `./README.md` |
| validar pedido humano vago ou arriscado | `./prompts/hooks/validate-user-intent.md` |
| consultar memoria governada sob demanda | `./_memory/README.md` |
| sincronizar artefatos apos mudanca | `./governance/lifecycle/artifact-synchronization-policy.md` |
| consultar sync targets | `./governance/authoring/artifact-registry.md` |
| compor contexto | `./governance/composition/context-composition.md` |
| escolher agente | `./agents/README.md` |
| escolher rule | `./rules/README.md` |
| escolher skill | `./skills/README.md` |
| escolher prompt | `./prompts/README.md` |
| executar checkpoint | `./prompts/hooks/README.md` |
| consultar documentacao humana | `./docs/README.md` |
| validar regressao | `./evals/README.md` |
| acompanhar remediacao | `./docs/remediation/README.md` |

---

## Nucleo injetavel

Carregar sob demanda, por relevancia:

- `./governance/`
- `./agents/`
- `./rules/`
- `./skills/`
- `./prompts/`

---

## Fora da composicao padrao

Nao carregar por habito:

- `./docs/`
- `./evals/`
- `./_memory/`
- `./LICENSE`
- `./INDEX.md` depois que o contexto especifico estiver selecionado

---

## Limites

Este indice nao substitui normas, regras, prompts, skills, agentes, hooks ou READMEs locais.

Este indice nao lista todos os arquivos do repositorio.

Este indice nao define governanca primaria.

`./_memory/` nao e fonte normativa e nao deve ser carregado por padrao.
