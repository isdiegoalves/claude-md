# Revisão de Duas Perspectivas

> Técnica: **Self-Consistency** - Verificação múltipla de qualidade

---

## A Técnica das Duas Perspectivas

Ao avaliar seu próprio trabalho, apresente **duas visões opostas**:

1. **Perspectiva do Perfeccionista** - O que criticaria?
2. **Perspectiva do Pragmático** - O que aceitaria?

---

## Framework de Análise

### Perspectiva do Perfeccionista

"Se eu fosse um code reviewer ultra-rigoroso, o que eu criticaria?"

- Nomenclatura poderia ser mais clara?
- Há edge cases não tratados?
- A arquitetura poderia ser mais limpa?
- Testes poderiam ser mais abrangentes?

### Perspectiva do Pragmático

"Se eu tivesse um prazo apertado, o que realmente importa?"

- A funcionalidade principal funciona?
- Não introduziu bugs óbvios?
- Código é mantenível o suficiente?
- Documentação é suficiente para o contexto?

---

## Template de Review

```markdown
## Avaliação de Duas Perspectivas

### 👁️ Perspectiva do Perfeicionista
**Críticas:**
- [Ponto 1 que poderia ser melhor]
- [Ponto 2 que poderia ser mais elegante]
- [Ponto 3 de arquitetura]

**Severidade:** [Baixa/Média/Alta]

### ⚖️ Perspectiva do Pragmático
**Aceitações:**
- Funcionalidade entregue funciona corretamente
- Código não introduz débito técnico grave
- Dentro do escopo solicitado

**Trade-offs Aceitáveis:**
- [O que é aceitável não ser perfeito]

### 🎯 Recomendação
[Qual perspectiva deve prevalecer neste caso]

**Justificativa:**
[Por que estamos escolhendo este trade-off]
```

---

## Exemplo Completo

```markdown
## Avaliação: Feature de Exportação CSV

### Perspectiva do Perfeccionista
- CSV poderia ter formatação mais robusta (escaping de vírgulas)
- Deveria suportar encoding UTF-8 BOM para Excel
- Arquitetura mistura UI com lógica de exportação

### Perspectiva do Pragmático
- Exportação funciona para 95% dos casos de uso
- Código é legível e mantenível
- Dentro do escopo original (export simples)

### Decisão
Adotar perspectiva pragmática, mas documentar melhorias futuras.
```

---

## Quando Usar Cada Perspectiva

| Contexto | Perspectiva | Por quê? |
|----------|-------------|----------|
| MVP/Protótipo | Pragmático | Velocidade > Perfeição |
| Core System | Perfeccionista | Qualidade é crítica |
| Bug Fix | Pragmático | Correção rápida importa mais |
| Refactor | Perfeccionista | Momento de melhorar |
