# Follow References, Not Descriptions

**Technique:** Few-shot Prompting — o código existente do usuário é o conjunto de exemplos (shots) mais confiável disponível. Estudá-lo antes de construir é usar few-shot implícito.

## Regra

Quando o usuário aponta para código existente como referência:
1. Estude-o completamente antes de construir
2. Identifique os padrões: nomenclatura, estrutura, estilo, abstrações usadas
3. Replique esses padrões exatamente

O código funcionando do usuário é uma spec melhor do que a descrição em inglês dele.

## Por que isso importa

Descrições em linguagem natural são ambíguas. Código é preciso. Um componente existente mostra exatamente como o usuário quer tratar erros, nomear variáveis, estruturar props — sem ambiguidade. Ignorar essa referência é a principal causa de "esse não é o estilo que usamos aqui."

## Sinal de aplicação

- Usuário diz "faça igual ao X" ou "siga o padrão do Y"
- Existe código similar já implementado no projeto
- Instrução menciona um arquivo ou componente específico como modelo
