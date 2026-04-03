# Spec-Based Development

**Technique:** Chain-of-Thought Prompting — entrevistar o usuário antes de escrever código força raciocínio explícito sobre requisitos, eliminando suposições que geram retrabalho.

## Regra

Para features não-triviais (3+ passos ou decisões arquiteturais):

1. Entre em plan mode
2. Use `AskUserQuestion` para entrevistar o usuário sobre:
   - Implementação técnica
   - UX e comportamento esperado
   - Preocupações e restrições
   - Trade-offs aceitáveis
3. Escreva a spec detalhada
4. A spec vira o contrato — execute contra ela, não contra suposições

**Elimine todas as suposições antes de tocar no código.**

## Por que isso importa

Suposições silenciosas são a principal causa de retrabalho. Uma spec de 10 minutos evita um refactor de 2 horas. O agente tem viés para iniciar rápido — esta regra corrige esse viés.

## Sinal de aplicação

- Feature envolve 3+ passos distintos
- Decisão arquitetural sem precedente claro no projeto
- Instrução do usuário admite múltiplas interpretações válidas
