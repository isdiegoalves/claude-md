# File System as State

**Technique:** Prompt Chaining — usar o sistema de arquivos como memória persistente entre passos encadeados, reduzindo pressão sobre a janela de contexto.

## Regra

O sistema de arquivos é a ferramenta de propósito geral mais poderosa disponível. Pare de manter tudo em contexto. Use ativamente:

### Leitura inteligente
Não carregue arquivos grandes cegamente no contexto. Use bash para grep, search, tail e leitura seletiva. Busca agêntica (encontrar seu próprio contexto) supera carregamento passivo de contexto.

### Resultados intermediários
Escreva resultados intermediários em arquivos. Isso permite múltiplas passagens sobre um problema e ancora os resultados em dados reproduzíveis.

### Processamento de dados grandes
Para operações com dados grandes: salve no disco e use ferramentas bash (`grep`, `jq`, `awk`) para buscar e processar. O bash é o instrumento mais poderoso disponível — use para qualquer coisa que se beneficie de scripting, incluindo encadeamento de chamadas de API e processamento de logs.

### Memória entre sessões
Use o sistema de arquivos para memória entre sessões: escreva resumos, decisões e trabalho pendente em arquivos markdown que persistam.

### Debugging reproduzível
Ao debugar: salve logs e outputs em arquivos para verificar contra artefatos reproduzíveis.

### Estrutura como contexto
Habilite progressive disclosure: arquivos de referência podem apontar para outros arquivos. Estrutura reduz pressão de contexto. A própria estrutura de pastas é uma forma de context engineering.

## Por que isso importa

Contexto em memória é volátil, limitado e sujeito a decay. O sistema de arquivos é persistente, ilimitado e indexável. O agente que usa arquivos como estado ativo consegue trabalhar em problemas muito maiores que sua janela de contexto.
