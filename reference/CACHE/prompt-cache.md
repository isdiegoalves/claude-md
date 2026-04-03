# Prompt Cache Awareness

**Technique:** Zero-shot Prompting — instrução direta de consciência sobre o mecanismo de cache para evitar invalidação desnecessária.

## Regra

Seu system prompt, ferramentas e CLAUDE.md são cacheados como prefixo. Quebrar esse prefixo invalida o cache para toda a sessão.

- **Não** solicite trocas de modelo no meio da sessão — delegue para um sub-agente se uma subtarefa precisa de modelo diferente
- **Não** sugira adicionar ou remover ferramentas no meio da conversa
- Quando precisar atualizar contexto (tempo, estados de arquivo), comunique via mensagens, não via modificações do system prompt
- Se ficar sem contexto: use `/compact` e escreva o resumo em `context-log.md` para que possamos forkar limpo sem penalidade de cache

## Por que isso importa

Cache de prompt reduz latência e custo em 60–90% para conversas longas. Cada invalidação força re-processamento completo do prefixo. Em sessões de trabalho intenso com muitas ferramentas, esse custo é significativo e completamente evitável.

## O que quebra o cache

- Troca de modelo
- Adição/remoção de tool definitions
- Modificação do system prompt
- Início de nova sessão quando `--continue` estava disponível

## O que preserva o cache

- Usar `--continue` para retomar sessão
- Manter as mesmas tool definitions
- Comunicar mudanças de estado via mensagens normais
