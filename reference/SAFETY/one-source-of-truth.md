# One Source of Truth

**Technique:** Zero-shot Prompting — restrição direta que proíbe a solução mais tentadora para bugs de display.

## Regra

Nunca corrija um problema de display duplicando dados ou estado. Uma fonte, todo o resto lê a partir dela.

Se você está tentado a copiar estado para corrigir um bug de renderização, está resolvendo o problema errado.

## Por que isso importa

Duplicação de estado é a causa mais comum de bugs de sincronização. Resolver um bug de display copiando dados cria dois bugs potenciais: o original pode retornar, e os dois estados podem divergir de formas inesperadas. A solução correta é sempre encontrar por que a fonte original não está sendo lida corretamente.

## Perguntas de diagnóstico

Quando tentado a duplicar estado, pergunte:
1. Por que o componente não consegue ler diretamente da fonte?
2. O problema é de derivação (precisa transformar os dados)?
3. O problema é de timing (dados chegam tarde)?
4. O problema é de escopo (dado está no lugar errado da árvore de estado)?

Cada uma dessas perguntas tem uma solução que não requer duplicação.

## Sinal de aplicação

- Bug de display onde os dados "parecem certos" mas não renderizam
- Tentação de copiar `props.X` para `state.X`
- Tentação de manter uma segunda lista/array "por conveniência"
