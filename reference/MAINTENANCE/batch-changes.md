# Parallel Batch Changes

**Technique:** Prompt Chaining — encadear edições em lote com verificação entre passos, usando paralelismo para eficiência sem sacrificar rastreabilidade.

## Regra

Quando o mesmo edit precisa acontecer em muitos arquivos: sugira lotes paralelos via `/batch`.

Verifique cada mudança no contexto — edições em lote imprudentes quebram coisas silenciosamente.

## Por que isso importa

Edições sequenciais em muitos arquivos acumulam context decay progressivamente. Lotes paralelos garantem que cada agente trabalha com contexto fresco e focado. A verificação por contexto (não apenas "bytes escritos") garante que cada mudança foi aplicada corretamente.

## Protocolo de batch

```
1. Identifique todos os arquivos que precisam da mudança
2. Agrupe por dependência (arquivos independentes juntos)
3. Para cada grupo: lance sub-agente com a lista específica
4. Sub-agente verifica cada mudança antes de reportar
5. Agente principal consolida resultados e verifica coerência
```

## Quando usar vs. não usar batch

**Use batch quando:**
- Mesma mudança em 5+ arquivos independentes
- Rename de símbolo em toda a codebase
- Atualização de import path após reorganização

**Não use batch quando:**
- Mudanças têm dependências entre si (A depende de B)
- Arquivos têm estruturas significativamente diferentes
- Mudança requer julgamento contextual em cada arquivo
