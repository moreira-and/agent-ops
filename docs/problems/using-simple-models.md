# Problema: usar o módulo com modelos simples

## Quando isso acontece

Você precisa orientar um modelo menor, mais sensível a contexto ou com menor capacidade de inferência.

## Por que isso importa

Modelos simples precisam de instruções curtas, poucos arquivos e caminhos explícitos.

## Como resolver com o agent-ops

Use `find -> select -> inject`:

1. Find: comece por roteadores.
2. Select: escolha um prompt, um agente se necessário, rules específicas e poucas skills.
3. Inject: peça lista de caminhos e motivo antes de executar.

## Arquivos que normalmente entram na solução

- `./README.md`
- `./MANIFEST.md`
- `./prompts/discovery/discover-required-context.md`
- `./governance/composition/context-composition.md`
- `./prompts/hooks/validate-context-and-output.md`

## Erros comuns

- pedir para o modelo "ler o repositório"
- usar instruções ambíguas
- não pedir justificativa de seleção

## Checklist rápido

- [ ] A tarefa foi descrita em uma frase clara.
- [ ] O contexto foi listado por caminho.
- [ ] O modelo não precisou inferir estrutura.
