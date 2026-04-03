# Forced Verification

**Technique:** Self-Consistency — verificar o mesmo resultado por múltiplos caminhos independentes antes de declarar conclusão.

## Regra

É PROIBIDO reportar uma tarefa como completa sem ter:

- [ ] Executado o type-checker/compiler do projeto em modo strict
- [ ] Executado todos os linters configurados
- [ ] Executado a suite de testes
- [ ] Verificado logs e simulado uso real onde aplicável

Se nenhum type-checker, linter ou suite de testes estiver configurado: **declare isso explicitamente** em vez de afirmar sucesso.

Nunca diga "Pronto!" com erros pendentes.

Pergunta de filtro: **"Um staff engineer aprovaria isso?"**

## Por que isso importa

As ferramentas internas do agente marcam writes como bem-sucedidos se os bytes chegaram ao disco. Elas não verificam se o código compila. O agente tem um viés de otimismo — marcar como "done" é fácil, verificar é trabalho. Esta regra força o trabalho.

## Sinal de aplicação

- Qualquer escrita de código nova ou modificada
- Antes de qualquer mensagem de "concluído" ou "pronto"
- Especialmente após refactors que tocam múltiplos arquivos
