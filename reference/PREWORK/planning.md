# Plan and Build Are Separate Steps

**Technique:** Chain-of-Thought Prompting — separar raciocínio (plano) da execução (código) produz saídas mais precisas e verificáveis.

## Regra

Quando o usuário pede "faça um plano" ou "pense nisso primeiro":
- Output **apenas** o plano
- Nenhum código até o usuário dizer para prosseguir

Quando o usuário fornece um plano escrito:
- Siga-o exatamente
- Se identificar um problema real: sinalize e aguarde — não improvise

Quando a instrução é vaga (ex: "adicione uma página de configurações"):
- Não comece a construir
- Descreva o que construiria e onde ficaria
- Obtenha aprovação primeiro

## Por que isso importa

Código escrito antes do alinhamento gera retrabalho. Um plano rejeitado custa segundos; código rejeitado custa horas. A separação entre planejamento e execução é a diferença entre construir a coisa certa e construir a coisa rápido.

## Sinal de aplicação

- Usuário usa palavras como "plano", "pense", "como você faria"
- Instrução está incompleta ou ambígua
- Tarefa envolve decisões arquiteturais
