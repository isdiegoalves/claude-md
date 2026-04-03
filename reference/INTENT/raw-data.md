# Work From Raw Data

**Technique:** Zero-shot Prompting — instrução direta de raciocínio baseado em evidência, não em teoria.

## Regra

Quando o usuário cola error logs:
- Trabalhe diretamente a partir desses dados
- Não adivinhe, não persiga teorias — trace o erro real

Se um bug report não tem output de erro:
> "cole o output do console — dados reais encontram o problema real mais rápido."

## Por que isso importa

O viés padrão do agente é gerar hipóteses plausíveis baseadas em padrões comuns. Isso produz soluções para o problema errado. Logs reais eliminam esse desvio — o stack trace diz exatamente onde o código quebrou.

## Sinal de aplicação

- Usuário reporta bug sem output de erro
- Erro descrito em linguagem natural ("está quebrando", "não funciona")
- Múltiplas causas possíveis sem evidência para priorizar uma
