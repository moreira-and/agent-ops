# core-principles

## Tipo do artefato

governance

## Finalidade

Definir os princípios fundacionais do `agent-ops`.

Este arquivo é a fonte primária dos princípios estruturais permanentes do repositório.

---

## Quando usar

Use este arquivo quando precisar:

- orientar decisões estruturais
- avaliar se um novo artefato deve existir
- validar fronteiras entre diretórios
- revisar coerência do crescimento do `agent-ops`

---

## Quando não usar

Não use este arquivo como fonte primária para:

- ordem detalhada de composição de contexto
- padrão de autoria de Markdown
- política de criação e remoção de artefatos
- checklist de qualidade

Consulte, respectivamente:

- `../composition/context-composition.md`
- `../authoring/markdown-authoring-standard.md`
- `../lifecycle/artifact-lifecycle-policy.md`
- `../quality/artifact-quality-standard.md`

---

## Dependências relacionadas

- `../../MANIFEST.md`

---

## Princípios

### 1. Responsabilidade única em Markdown
Cada arquivo `.md` MUST possuir uma responsabilidade principal clara.

Se um artefato responder a múltiplas perguntas centrais, ele SHOULD ser dividido.

Um arquivo MUST NOT misturar responsabilidades centrais como:

- prompt + rule
- agent + skill
- governance + rule de output
- documentação humana + instrução injetável
- histórico de execução + norma reutilizável

---

### 2. Fonte primária única
Cada tipo de informação MUST possuir uma única fonte primária dentro do `agent-ops`.

Arquivos secundários MAY apontar para essa fonte, mas MUST NOT competir com ela.

---

### 3. Crescimento por decomposição
O repositório MUST crescer por decomposição controlada e referência.

O repositório MUST NOT crescer por cópia de conteúdo entre arquivos.

O `agent-ops` MUST ser aberto para novos prompts, agents, rules, skills e hooks, mas fechado contra mudanças que quebrem `find -> select -> inject`.

Novos conhecimentos SHOULD ser plugáveis por artefatos especializados, sem reescrever arquivos centrais sem necessidade.

---

### 4. Substituição por categoria
Arquivos do mesmo tipo SHOULD ser substituíveis dentro da mesma categoria sem quebrar o fluxo.

Um `agent` MUST continuar sendo perfil executor.

Uma `skill` MUST continuar sendo capacidade operacional reutilizável.

Uma `rule` MUST continuar sendo restrição de output.

Um `prompt` MUST continuar sendo ponto de entrada.

Um artefato que exigir comportamento excepcional demais SHOULD ser reclassificado, dividido ou movido.

---

### 5. Segregação de interface contextual
Nenhum agente SHOULD ser obrigado a carregar contexto que não precisa.

A composição MUST permitir seleção mínima por tarefa.

Artefatos SHOULD evitar:

- conteúdo genérico excessivo
- múltiplas capacidades não relacionadas
- várias famílias de regra no mesmo arquivo
- prompts que embutem governança, agente, regras e técnicas

---

### 6. Inversão de dependência contextual
Prompts, agents, skills e rules MUST depender de contratos explícitos e caminhos declarados.

Eles MUST NOT depender de memória externa, leitura indiscriminada do repositório ou arquivos carregados por acaso.

Artefatos de alto nível MUST NOT copiar conteúdo de artefatos especializados quando uma referência por caminho for suficiente.

---

### 7. Mínima injeção necessária
A composição de contexto MUST priorizar apenas o contexto necessário para a tarefa.

Conteúdo opcional MUST ser carregado apenas quando houver relevância clara.

---

### 8. Referência explícita por caminho
Dependências entre artefatos MUST ser declaradas por caminho.

Referências vagas SHOULD ser evitadas.

---

### 9. Legibilidade para humanos e agentes
Todo arquivo MUST ser compreensível tanto para humanos quanto para LLMs.

Isso implica:

- propósito claro
- escopo claro
- limites claros
- dependências claras
- baixa ambiguidade

---

### 10. Fronteiras explícitas
Cada diretório MUST ter fronteira clara.

Quando houver sobreposição entre áreas, a fonte primária correta MUST prevalecer.

---

### 11. Governança antes de expansão
A expansão do repositório SHOULD preservar governança antes de aumentar volume.

Se uma nova adição piorar clareza, manutenção ou seleção, ela SHOULD NOT ser feita.

---

### 12. Modularidade útil
A modularidade MUST melhorar pelo menos um dos seguintes fatores:

- recuperação
- seleção
- manutenção
- governança
- clareza
- redução de alucinação

Fragmentação sem ganho real SHOULD NOT ocorrer.

---

### 13. Lacunas devem ser explicitadas
Se faltar contexto crítico, o agente SHOULD explicitar a lacuna em vez de inventar conteúdo.

---

## Injeção de dependências em Markdown

O contexto MUST ser composto por injeção seletiva de arquivos `.md`.

A composição correta é:

```txt
find -> select -> inject
```

Isso significa:

- `find`: localizar artefatos candidatos com base na tarefa
- `select`: escolher somente os artefatos necessários
- `inject`: montar a janela de contexto na ordem oficial

A injeção MUST ser explícita, mínima e rastreável.

---

## Anti-patterns de acoplamento contextual

São sinais de acoplamento ruim:

- prompt que só funciona se o agente lembrar regras externas
- skill que repete regra pertencente a `../../rules/`
- agent que embute procedimento pertencente a `../../skills/`
- rule que depende de contexto não declarado
- README com norma que pertence a `../../MANIFEST.md`
- conceito simples que exige leitura conjunta de vários arquivos sem necessidade

---

## Limites

Este arquivo define princípios fundacionais.

Este arquivo não substitui:

- regras de composição
- padrão de autoria
- política de lifecycle
- padrão de qualidade
