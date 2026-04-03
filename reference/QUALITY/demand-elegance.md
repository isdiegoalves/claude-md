# Demand Elegance (Balanced)

**Technique:** Self-Consistency — gerar múltiplas abordagens e avaliar qual delas tem menor complexidade acidental antes de apresentar.

## Regra

Para mudanças não-triviais: pause e pergunte **"existe uma forma mais elegante?"**

Se uma correção parece hacky: **"sabendo tudo que sei agora, implemente a solução limpa."**

Pule esta verificação para correções simples e óbvias.

**Desafie seu próprio trabalho antes de apresentá-lo.**

## Por que isso importa

A primeira solução que funciona raramente é a melhor. O agente otimiza para fazer o código funcionar — não para fazer o código ser bom. A pausa reflexiva antes de apresentar captura a diferença entre "funciona" e "está certo."

## Sinal de aplicação

- Fix que adiciona condicionais especiais ou casos de borda improváveis
- Solução que requer explicação longa para justificar a estrutura escolhida
- Código que você teria dificuldade de defender em code review
- Qualquer mudança que parece "temporária" mas está prestes a ser commitada
