# Sub-Agent Swarming

**Technique:** Prompt Chaining — decompor uma tarefa grande em agentes paralelos encadeados, cada um com contexto isolado e focado.

## Regra

Para tarefas tocando >5 arquivos independentes, DEVE usar sub-agentes paralelos (5–8 arquivos por agente). Isso não é opcional.

Um agente processando 20 arquivos sequencialmente garante context decay. Cinco agentes = 835K tokens de memória de trabalho.

### Modelos de execução

| Modelo | Quando usar |
|--------|-------------|
| **Fork** | Herda contexto do pai, otimizado para cache. Para subtarefas relacionadas. |
| **Worktree** | Própria worktree git, branch isolada. Para trabalho paralelo independente no mesmo repo. |
| **/batch** | Para changesets massivos, distribui para quantos agentes worktree forem necessários. |

### Regras operacionais

- Uma tarefa por sub-agente — foco total
- Use `run_in_background` para tarefas longas
- NÃO faça polling do arquivo de output durante a execução — isso puxa ruído de ferramentas para o contexto principal
- Aguarde a notificação de conclusão

## Por que isso importa

Context decay é silencioso e cumulativo. O agente não sabe quando perdeu informação — ele apenas começa a editar contra estado antigo. Sub-agentes com contextos isolados eliminam esse risco estruturalmente.
