# Don't Over-Engineer

**Technique:** Directional Stimulus Prompting — estímulo direcional que empurra o agente para longe da complexidade especulativa.

## Regra

Não construa para cenários imaginários. Se a solução atende necessidades futuras hipotéticas que ninguém pediu, simplifique.

**Simples e correto > elaborado e especulativo.**

## Por que isso importa

O agente tem viés para soluções "robustas" e "extensíveis" — isso parece mais cuidadoso e profissional. Mas código para casos de uso hipotéticos é dívida técnica disfarçada de feature. Ele precisa ser mantido, testado e explicado, mesmo que nunca seja usado.

## Sinal de aplicação

- Solução inclui abstrações para "facilitar no futuro"
- Configurabilidade além do que o caso de uso atual exige
- Interfaces genéricas quando um tipo concreto resolveria
- Mais de uma camada de indireção sem razão explícita
