# Execução em Fases

**Padrão:** Prompt Chaining
**Fonte:** CLAUDE.md Seção 1 - Pré-Trabalho

> Nunca tente refatorações multi-arquivo em uma única resposta. Divida o trabalho em fases explícitas. Complete a Fase 1, execute a verificação e aguarde aprovação explícita antes da Fase 2. Cada fase deve tocar no máximo 5 arquivos.

---

## Template de Checklist Copiavel

### Checklist de Fase

```markdown
## Phase [N]: [Nome da Fase]

**Objetivo:** [Descrever o objetivo desta fase]
**Arquivos:** [Listar maximo 5 arquivos]

### Checklist de Execucao

- [ ] 1. [Primeira tarefa da fase]
- [ ] 2. [Segunda tarefa da fase]
- [ ] 3. [Terceira tarefa da fase]
- [ ] 4. [Quarta tarefa da fase]
- [ ] 5. [Quinta tarefa da fase]

### Verificacao Obrigatoria

- [ ] Executado `npx tsc --noEmit` (type-check)
- [ ] Executado `npx eslint . --quiet` (lint)
- [ ] Todos os erros corrigidos
- [ ] Testes passam (se aplicavel)

### Aguardando Aprovacao

- [ ] Usuario revisou as mudancas
- [ ] Usuario aprovou proxima fase
- [ ] Proceder para Phase [N+1]
```

---

## Regras Fundamentais

### Limite de 5 Arquivos por Fase

| Regra | Descricao | Por que? |
|-------|-----------|----------|
| **Hard limit** | Maximo 5 arquivos modificados por fase | Mantem contexto sob controle |
| **Independencia** | Fases devem ser independentes quando possivel | Permite revisao isolada |
| **Atomicidade** | Cada fase deve deixar o codigo em estado funcional | Nao quebrar builds entre fases |

### Exemplos de Divisao por Fase

**Cenario: Refactor de 15 arquivos**

```
❌ Errado: Fase unica modificando 15 arquivos de uma vez
✅ Correto:
   - Phase 1: Arquivos 1-5 (preparacao)
   - Phase 2: Arquivos 6-10 (migracao principal)
   - Phase 3: Arquivos 11-15 (limpeza e finalizacao)
```

**Cenario: Adicionar nova feature complexa**

```
❌ Errado: Tudo em uma resposta
✅ Correto:
   - Phase 1: Setup e interfaces (tipos, contratos)
   - Phase 2: Implementacao core (logica principal)
   - Phase 3: Integracao e UI (componentes, views)
   - Phase 4: Testes e documentacao
```

---

## Processo de Verificacao Entre Fases

### Checklist de Verificacao

Antes de solicitar aprovacao para proxima fase:

```markdown
## Verificacao Pos-Fase

### Validacao Tecnica
- [ ] Type-check: `npx tsc --noEmit`
- [ ] Lint: `npx eslint . --quiet`
- [ ] Testes: `npm test` (ou equivalente)
- [ ] Build: `npm run build` (se aplicavel)

### Validacao de Qualidade
- [ ] Nenhum codigo morto introduzido
- [ ] Nenhum console.log de debug
- [ ] Codigo segue padroes do projeto
- [ ] Estados estao consistentes

### Validacao de Contexto
- [ ] Mensagens de commit claras
- [ ] Nenhuma referencia quebrada
- [ ] Imports/exports consistentes
```

---

## Protocolo de Aprovacao

### O Que Esperar do Usuario

1. **Revisao**: O usuario deve revisar as mudancas da fase atual
2. **Feedback**: O usuario pode solicitar ajustes antes da proxima fase
3. **Aprovacao explicita**: Aguardar "yes", "go", "do it", "proceed" ou similar
4. **Nunca assumir**: Nao iniciar proxima fase sem confirmacao clara

### Exemplo de Dialogo

```markdown
Agente: Phase 1 completa. Modifiquei:
  - src/types/user.ts
  - src/api/user.ts
  - src/hooks/useUser.ts

Verificacao: Type-check e lint passaram.
Aguardando sua aprovacao para iniciar Phase 2.

Usuario: go

Agente: [Inicia Phase 2 imediatamente, sem repeticao do plano]
```

---

## Fluxo de Trabalho Completo

```text
+--------------------------------------------------------------+
|  INICIO: Tarefa identificada (ex: refactor multi-arquivo)    |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  1. PLANEJAMENTO                                             |
|     • Quebrar em fases                                       |
|     • Maximo 5 arquivos por fase                             |
|     • Definir ordem de dependencia                           |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  2. EXECUTAR PHASE N                                         |
|     • Modificar arquivos da fase                             |
|     • Executar verificacoes tecnicas                         |
|     • Garantir estado funcional                                |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  3. APRESENTAR RESULTADOS                                    |
|     • Listar arquivos modificados                            |
|     • Resumo das mudancas                                    |
|     • Status das verificacoes                                |
|     • Perguntar: "Aprovar para proxima fase?"                  |
+--------------------------------------------------------------+
                               |
                               v
                    +--------------------+
                    |  Aguardando Input  |
                    +--------------------+
                               |
              +----------------+----------------+
              |                                 |
              v                                 v
+-------------------------+        +-------------------------+
|  "yes/go/do it/proceed" |        |  "ajuste X" / feedback   |
+-------------------------+        +-------------------------+
              |                                 |
              v                                 v
+-------------------------+        +-------------------------+
|  Iniciar Phase N+1      |        |  Fazer ajustes          |
|  (nao repetir plano)    |        |  Re-verificar            |
+-------------------------+        +-------------------------+
```

---

## Prompt Template para Agentes

Use este prompt para instruir qualquer agente sobre este workflow:

```markdown
## Prompt Chaining: Execucao em Fases

Para tarefas multi-arquivo:

1. Divida o trabalho em fases explicitas
2. Cada fase deve tocar NO MAXIMO 5 arquivos
3. Complete a fase atual completamente
4. Execute verificacao tecnica (type-check, lint)
5. Aguarde aprovacao explicita do usuario antes da proxima fase
6. Ao receber "yes/go/do it", proceda imediatamente sem repetir o plano

Nunca tente refatoracoes multi-arquivo em uma unica resposta.
```
