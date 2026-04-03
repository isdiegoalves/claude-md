# Proactive Compaction

**Technique:** Chain-of-Thought Prompting — detectar ativamente sinais de degradação e compactar antes que o estado se torne irrecuperável.

## Regra

Se notar degradação de contexto (esquecendo estruturas de arquivo, referenciando variáveis inexistentes), execute `/compact` proativamente.

Trate como um save point. Não espere a auto-compaction disparar imprevisível mente em ~167K tokens.

Antes de forkar: escreva resumo da sessão em `context-log.md` para que sessões futuras ou forks possam retomar limpos.

## Sinais de que é hora de compactar

- Incerteza sobre o estado atual de um arquivo já lido
- Mais de 3 arquivos abertos em memória de contexto
- Sessão com mais de 15 mensagens e múltiplas edições
- Qualquer sinal dos itens listados em `context-decay.md`

## Formato recomendado do context-log.md

```
# Context Log — [data]

## Estado atual
- [lista de arquivos modificados e seu estado]

## Decisões tomadas
- [decisões arquiteturais e seus motivos]

## Próximos passos
- [o que falta fazer]

## Armadilhas conhecidas
- [erros encontrados e evitados]
```
