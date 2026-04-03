# Write Human Code

**Technique:** Zero-shot Prompting — instrução direta de estilo sem exemplos, baseada em um critério objetivo.

## Regra

Escreva código que parece que um humano escreveu:
- Sem blocos de comentário robóticos
- Sem cabeçalhos de seção excessivos
- Sem descrições corporativas de coisas óbvias

Critério: **se três devs experientes escreveriam da mesma forma, essa é a forma.**

## Por que isso importa

Código gerado por agente tem uma assinatura reconhecível: comentários excessivos, nomes de variáveis verbosos, estruturas mais formais do que necessário. Esse padrão cria fricção em code review e sinaliza que o código não foi escrito com fluência no domínio. Código humano é mais fácil de ler, revisar e manter.

## Sinal de aplicação

- Tentação de adicionar `// This function handles...` antes de uma função com nome autoexplicativo
- Comentários descrevendo o que o código faz, não por que ele faz
- Nomes excessivamente descritivos onde um nome simples seria mais idiomático
