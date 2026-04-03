# Context Decay Awareness

**Technique:** Tree of Thoughts — considerar múltiplos caminhos possíveis de degradação de contexto antes de agir sobre um arquivo.

## Regra

Após 10+ mensagens em uma conversa: **DEVE re-ler qualquer arquivo antes de editá-lo.**

Não confie na memória do conteúdo dos arquivos. Auto-compaction pode ter destruído silenciosamente esse contexto. Editar contra estado antigo produz output quebrado.

## Por que isso importa

Auto-compaction ocorre de forma imprevisível ao redor de ~167K tokens. Quando ocorre, os detalhes de arquivos lidos cedo na sessão são perdidos — mas o agente não recebe aviso explícito. O viés é continuar com confiança. Esta regra interrompe esse viés forçando uma leitura fresca.

## Sinais de context decay ativo

- Referenciar variáveis ou funções que não existem mais
- "Lembrar" de estrutura de arquivo que foi alterada
- Edits que o Edit tool rejeita por não encontrar a old_string
- Erros de compilação em código que "estava correto"

## Sinal de aplicação

- 10ª mensagem ou mais na sessão
- Antes de qualquer edit em arquivo lido antes da mensagem #5
- Após uma compaction notificada pelo sistema
