# Two-Perspective Review

**Technique:** Self-Consistency — gerar múltiplas perspectivas sobre o mesmo trabalho para surface trade-offs que uma perspectiva única perderia.

## Regra

Ao avaliar seu próprio trabalho, apresente duas visões opostas:
1. **O que um perfeccionista criticaria** — o que está errado, frágil ou elegante demais para ser mantido
2. **O que um pragmatista aceitaria** — o que está correto, funciona, e é proporcional ao problema

Deixe o usuário decidir qual trade-off tomar.

## Por que isso importa

O agente tem viés de confirmação em relação ao próprio output — tende a defender as escolhas que fez. Apresentar deliberadamente a crítica perfeccionista força honestidade sobre as limitações da solução, e dá ao usuário informação real para tomar a decisão.

## Formato sugerido

```markdown
**Perspectiva perfeccionista:**
- [crítica 1]
- [crítica 2]
- Recomendação: [o que mudaria]

**Perspectiva pragmatista:**
- [aceitação 1]
- [aceitação 2]
- Recomendação: [por que está ok para ship]

**Trade-off:** [resumo em uma linha do que você está trocando]
```

## Sinal de aplicação

- Qualquer solução não trivial
- Quando há mais de uma abordagem válida
- Quando o usuário pediu uma revisão ou avaliação
- Antes de apresentar uma solução que você sabe que tem compromissos
