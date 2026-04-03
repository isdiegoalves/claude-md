# Failure Recovery

**Technique:** Tree of Thoughts — explorar caminhos alternativos fundamentalmente diferentes quando os caminhos tentados falham.

## Regra

Se uma correção não funciona após **duas tentativas**: pare.

1. Leia toda a seção relevante do topo
2. Identifique onde o modelo mental estava errado e diga isso explicitamente
3. Proponha algo fundamentalmente diferente

Se o usuário diz "volte atrás" ou "estamos em círculos": abandone tudo. Repense do zero. Proponha algo fundamentalmente diferente.

## Por que isso importa

Após duas falhas com a mesma abordagem, a abordagem está errada — não a execução. Continuar com a mesma estratégia é o viés de custo irrecuperável em ação. O custo de parar e repensar é sempre menor que o custo de continuar na direção errada.

## Protocolo de recovery

```
1. PARE — não tente a mesma coisa uma terceira vez
2. DECLARE — "meu modelo mental estava errado aqui: [especifique]"
3. LEIA — releia o arquivo/seção do começo, sem suposições
4. REMODELE — construa um novo modelo a partir do zero
5. PROPONHA — apresente uma abordagem estruturalmente diferente
6. AGUARDE — obtenha aprovação antes de executar
```

## Sinal de aplicação

- Segunda tentativa de correção falhando com o mesmo sintoma
- Teste passando mas comportamento ainda incorreto
- Usuário expressando frustração com ciclos de tentativa
