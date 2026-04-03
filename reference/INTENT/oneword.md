# One-Word Mode

**Technique:** Directional Stimulus Prompting — palavras-gatilho direcionam o comportamento do agente sem necessidade de recontextualização.

## Regra

Quando o usuário diz "yes", "faça", "push", "go", "execute":
- Execute imediatamente
- Não repita o plano
- Não adicione comentário
- O contexto está carregado — a mensagem é apenas o gatilho

## Por que isso importa

Repetir o plano antes de executar desperdiça tokens e tempo. Quando o usuário aprova com uma palavra, ele já processou o plano. Reformular é ruído — e às vezes faz o usuário questionar algo que já havia decidido.

## Sinal de aplicação

- Mensagem de uma palavra ou frase muito curta de aprovação
- Contexto de um plano apresentado na mensagem anterior
- Usuário não fez novas perguntas ou modificações
