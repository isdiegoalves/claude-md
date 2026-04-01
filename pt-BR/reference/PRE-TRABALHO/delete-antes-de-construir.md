# Passo 0: Delete Antes de Construir

**Padrão:** Zero-shot Prompting
**Fonte:** CLAUDE.md Seção 1 - Pré-Trabalho

> Código morto acelera a compactação de contexto. Antes de QUALQUER refatoração estrutural em um arquivo >300 LOC, primeiro remova todas as props mortas, exports não utilizados, imports não utilizados e logs de debug. Faça commit desta limpeza separadamente antes de iniciar o trabalho real. Após qualquer reestruturação, delete qualquer coisa agora não utilizada. Sem fantasmas no projeto.

---

## Checklist Pré-Refator

Copie e cole este checklist antes de iniciar qualquer refatoração estrutural:

```markdown
## Checklist de Cleanup Pré-Refator

- [ ] Identifique arquivo(s) alvo >300 LOC
- [ ] Verifique props mortas (propriedades de componente não usadas)
- [ ] Verifique exports não usados (funções, constantes, tipos)
- [ ] Verifique imports não usados
- [ ] Verifique logs de debug (console.log, declarações de debug)
- [ ] Remova todo o código morto identificado
- [ ] Commit de limpeza: `git commit -m "cleanup: remove dead code before refactor"`
- [ ] Prossiga com o refator estrutural
```

---

## Regras de Limpeza de Codigo Morto

### O que Remover

| Categoria | Exemplos | Como Identificar |
|-----------|----------|------------------|
| **Dead Props** | Props declaradas mas nunca usadas no componente | Buscar por props nao referenciadas no corpo do componente |
| **Unused Exports** | `export const helper = ...` nunca importado em outro lugar | Verificar se ha imports do simbolo em outros arquivos |
| **Unused Imports** | `import { unused } from './module'` | Linhas cinzas no VS Code ou `organize imports` |
| **Debug Logs** | `console.log`, `console.debug`, `debugger;` | Buscar por `console.` e `debugger` |
| **Codigo Comentado** | Blocos de codigo comentados | Buscar por `/* ... */` e `//` seguido de codigo |

### Thresholds

- **300 LOC**: Limiar critico. Arquivos maiores que 300 linhas devem passar por cleanup antes de qualquer refactor estrutural
- Metrica: Contar linhas de codigo (excluindo comentarios e linhas vazias)

### Processo de Commit

1. **Commit separado obrigatorio**: A limpeza DEVE ser commitada separadamente do refactor
2. **Mensagem padrao**: `cleanup: remove dead code before refactor`
3. Nao misturar alteracoes de cleanup com alteracoes de logica no mesmo commit

### Pos-Refactor

Apos qualquer reestruturacao:
- Re-executar a verificacao de codigo morto
- Verificar se simbolos exportados foram movidos para novos arquivos e os originais foram deletados
- Garantir: **Sem fantasmas no projeto**

---

## Fluxo de Trabalho Completo

```text
+-------------------------------------------------------------+
|  INICIO: Identificou arquivo >300 LOC para refactor         |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  1. EXECUTAR CHECKLIST DE CLEANUP                           |
|     • Dead props? → Remover                                 |
|     • Unused exports? → Remover                             |
|     • Unused imports? → Remover                               |
|     • Debug logs? → Remover                                   |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  2. COMMIT SEPARADO                                         |
|     git add .                                               |
|     git commit -m "cleanup: remove dead code before refactor" |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  3. EXECUTAR REFACTOR                                       |
|     (Agora sim, iniciar o trabalho estrutural)              |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  4. POS-REFACTOR VERIFICACAO                                |
|     • Novo codigo morto criado?                             |
|     • Arquivos antigos podem ser deletados?                 |
|     • Commits finais                                        |
+-------------------------------------------------------------+
```

---

## Prompt Template para Agentes

Use este prompt para instruir qualquer agente sobre este workflow:

```markdown
## Zero-Shot Instruction: Delete Antes de Construir

Antes de fazer qualquer refactor estrutural em arquivos >300 linhas, execute:

1. Identifique codigo morto: dead props, unused exports, unused imports, debug logs
2. Remova todo o codigo morto encontrado
3. Commit separado com mensagem: "cleanup: remove dead code before refactor"
4. Somente entao prossiga com o refactor solicitado

Threshold: 300 LOC e o limiar critico que dispara este workflow.
```
