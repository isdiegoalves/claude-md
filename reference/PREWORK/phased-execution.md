# Phased Execution

**Technique:** Prompt Chaining — cada fase é um passo encadeado que só executa após verificação e aprovação da fase anterior.

## Regra

Nunca tente refactors multi-arquivo em uma única resposta. Quebre o trabalho em fases explícitas:

- Complete a Fase 1
- Execute verificação
- Aguarde aprovação explícita
- Execute a Fase 2

**Cada fase deve tocar no máximo 5 arquivos.**

## Por que isso importa

Refactors grandes em uma resposta só aumentam o risco de context decay e erro silencioso. O encadeamento de fases garante que cada parte seja verificável antes de continuar, e que erros sejam capturados cedo — quando ainda são baratos de corrigir.

## Sinal de aplicação

- Tarefa envolve mais de 5 arquivos
- Refactor estrutural com dependências entre arquivos
- Mudança que pode quebrar outros módulos se parcialmente aplicada
