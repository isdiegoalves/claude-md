# Mudanças em Lote Paralelo

> Técnica: **Prompt Chaining**

---

## O Princípio

Quando a mesma edição precisar acontecer em muitos arquivos, sugira **lotes paralelos**.

- Verifique cada mudança em contexto
- Reckless bulk edits quebram coisas silenciosamente
- Dividir em batches permite verificação entre etapas

---

## Estratégia de Batches

### Divisão por Tipo

```
Batch A: Componentes UI (5-8 arquivos .tsx)
Batch B: Serviços/API (5-8 arquivos .ts)
Batch C: Testes (5-8 arquivos .test.ts)
```

### Divisão por Dependência

```
Batch 1: Interfaces e tipos (base)
Batch 2: Implementações que dependem de Batch 1
Batch 3: Componentes que dependem de Batch 2
```

---

## Checklist de Batch

### Antes
- [ ] Identifiquei todos os arquivos afetados
- [ ] Agrupei em batches de no máximo 5-8 arquivos
- [ ] Defini ordem de dependência entre batches

### Durante
- [ ] Executei verificação técnica após cada batch
- [ ] Confirmei que não quebrei nada no batch anterior
- [ ] Documentei mudanças para o próximo batch

### Após
- [ ] Verificação final em todos os arquivos modificados
- [ ] Testes passam
- [ ] Type-check limpo

---

## Exemplo: Rename em Massa

**Cenário:** Renomear `getUser` para `fetchUser` em 20 arquivos

```
❌ ERRADO: Editar todos 20 arquivos de uma vez

✅ CORRETO:
  Batch 1: API layer (api/user.ts, api/client.ts)
  Batch 2: Hooks (hooks/useUser.ts)
  Batch 3: Components (components/User*.tsx)
  Batch 4: Tests (*.test.ts)

  [Verificação entre cada batch]
```
