# Verifique Antes de Relatar

> Tecnica: **ReAct** (Reasoning + Acting + Verification)

---

## O Ciclo ReAct de Verificacao

Antes de declarar qualquer tarefa como "pronta", execute o ciclo completo de ReAct:

```
[Reason]  Por que estou verificando?
    |
    v
[Act]     Releia tudo que modificou
    |
    v
[Observe] O que mudou? O que permanece?
    |
    v
[Verify]  Confirmacao final
    |
    v
[Report]  So entao: "Pronto!"
```

---

## Checklist de Verificacao Pre-Report

### Revisao de Conteudo
- [ ] Nada referencia algo que nao existe mais
- [ ] Nada esta sem uso (dead code)
- [ ] Logica flui corretamente
- [ ] Imports/exports estao consistentes

### Revisao Tecnica
- [ ] Type-check: `npx tsc --noEmit` - CLEAN
- [ ] Lint: `npx eslint . --quiet` - CLEAN
- [ ] Testes passam (se aplicavel)
- [ ] Build bem-sucedido (se aplicavel)

### Revisao de Contexto
- [ ] Mensagens de commit claras e descritivas
- [ ] Arquivos relevantes foram todos verificados
- [ ] Nenhum arquivo "perdido" nas mudancas

---

## Template de Report

```markdown
## Tarefa Completa: [Nome da Tarefa]

### Arquivos Modificados
1. `src/file1.ts` - [mudanca]
2. `src/file2.ts` - [mudanca]

### Verificacao Realizada
- [x] Type-check: CLEAN
- [x] Lint: CLEAN
- [x] Testes: [X/Y passaram]

### O que foi verificado
- Nada referencia simbolos removidos
- Todos os imports estao resolvidos
- Logica principal funciona conforme esperado

**Status: Pronto para revisao**
```

---

## Anti-Patterns

❌ **NUNCA reporte:**
- "Pronto!" sem verificar
- "Acho que esta bom" (subjetivo)
- "Parece funcionar" (sem confirmacao)

✅ **SEMPRE reporte:**
- "Verificado: type-check e lint passaram"
- "Relei todos os arquivos modificados"
- "Status: [especifico do que foi verificado]"
