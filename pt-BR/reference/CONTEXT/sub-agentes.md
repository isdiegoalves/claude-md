# Enxame de Sub-Agentes

> Tecnica: **Prompt Chaining** | Source: CLAUDE.md §4

---

## Quando Usar

**ATIVAR quando:** Task toca >5 arquivos independentes

**OBRIGATORIO para:**
- Refactors multi-arquivo
- Adicao de features que afetam multiplos modulos
- Alteracoes em toda a base de codigo

**NAO opcional.** Um agente processando 20 arquivos sequencialmente garante context decay.

---

## Como Particionar

### Regra de Ouro: 5-8 arquivos por agente

| Total de Arquivos | Agentes Necessarios | Tokens Disponiveis |
|-------------------|--------------------|--------------------|
| 6-8 | 1 | ~167K |
| 9-16 | 2 | ~334K |
| 17-25 | 3-4 | ~501K-668K |
| 25+ | 5+ | 835K+ |

### Estrategias de Particionamento

**Por Dominio (Recomendado)**
```
Agente A: Componentes UI (5-8 arquivos .tsx)
Agente B: Logica de negocio (5-8 arquivos .ts)
Agente C: Utilitarios e helpers (5-8 arquivos)
```

**Por Dependencia**
```
Agente A: Interface e tipos (arquivos base)
Agente B: Implementacoes que dependem de A
Agente C: Testes e mocks
```

**Por Localizacao**
```
Agente A: src/features/auth/*
Agente B: src/features/dashboard/*
Agente C: src/shared/*
```

---

## Workflow de Orquestracao

### Phase 1: Analise e Planejamento
1. Mapear todos os arquivos afetados
2. Agrupar por coesao logica
3. Definir ordem de dependencias
4. Criar brief para cada agente

### Phase 2: Execucao Paralela
```
+-----------------------------------------+
| Agente Orquestrador |
| ( mantem visao global ) |
+--------------+--------------------------+
       |     |     |
       v     v     v
   +------+ +------+ +------+
   |Agente| |Agente| |Agente|
   | A | | B | | C |
   |5-8 | |5-8 | |5-8 |
   |files | |files | |files |
   +--+---+ +--+---+ +--+---+
      |        |        |
      +--------|--------+
               v
        +----------------+
        | Merge e |
        | Verificacao |
        +----------------+
```

### Phase 3: Integracao
1. Verificar conflitos entre resultados
2. Validar interfaces compartilhadas
3. Rodar testes end-to-end
4. Confirmar type-check global

---

## Checklist de Orquestracao

### Pre-Flight
- [ ] Liste EXATAMENTE quais arquivos serao modificados
- [ ] Agrupe em batches de 5-8 arquivos
- [ ] Identifique dependencias entre batches
- [ ] Defina qual agente executa primeiro (se houver deps)

### Para Cada Agente
- [ ] Brief claro com escopo definido
- [ ] Contexto suficiente (nao exagerar)
- [ ] Ponto de integracao definido
- [ ] Criterios de sucesso claros

### Pos-Execucao
- [ ] Todos os batches completaram?
- [ ] Interfaces entre batches consistentes?
- [ ] `npx tsc --noEmit` passa?
- [ ] Testes passam?

---

## Exemplo Pratico

**Cenario:** Refactor de 15 arquivos de autenticacao

```
❌ ERRADO:
   1 agente processa todos os 15 arquivos sequencialmente
   → Context decay no arquivo 10+
   → Bugs em arquivos finais

✅ CORRETO:
   Agente A: Tipos, interfaces, contratos (3 arquivos)
   Agente B: Hooks e servicos de auth (6 arquivos)
   Agente C: Componentes UI de login (6 arquivos)

   → Execucao paralela
   → 3 × 167K = 501K tokens efetivos
   → Cada arquivo com contexto fresco
```

---

## Anti-Patterns

| Problema | Solucao |
|----------|---------|
| Agente unico com >8 arquivos | Dividir em multiplos agentes |
| Batches sem criterio claro | Agrupar por dominio/dependencia |
| Overlap de contexto entre agentes | Definir interfaces claras |
| Orquestracao sincrona desnecessaria | Executar independentes em paralelo |
