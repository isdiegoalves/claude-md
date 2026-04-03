# Bug Autopsy

**Technique:** Reflexion — análise retrospectiva que transforma cada bug em um guardrail para o futuro.

## Regra

Após corrigir um bug: explique por que ele aconteceu e se algo poderia prevenir essa categoria de bug no futuro.

Não apenas corrija e siga em frente. Cada bug é um guardrail potencial.

## Estrutura de uma autopsia

```markdown
## Bug: [descrição]

**Causa raiz:** [o que tecnicamente causou o bug]
**Por que escapou:** [por que não foi detectado antes]
**Categoria:** [tipo de erro: race condition, null reference, type mismatch, etc.]
**Prevenção sistêmica:** [o que poderia ter evitado esta classe de bugs]
  - Tipo de teste que teria capturado
  - Validação que faltava
  - Padrão arquitetural que previne
```

## Por que isso importa

Bugs corrigidos sem análise são lições perdidas. O mesmo padrão de erro — race condition, assumption sobre estado externo, falta de validação de null — tende a se repetir no mesmo projeto. A autopsia converte o custo do bug em valor para o futuro.

## Sinal de aplicação

- Qualquer bug corrigido que não era óbvio na primeira leitura
- Bugs que passaram por testes existentes
- Bugs em código que "parecia correto"
