# Tool Result Blindness

**Technique:** Chain-of-Thought Prompting — raciocinar explicitamente sobre possível truncamento antes de confiar em resultados de busca.

## Regra

Resultados de ferramentas com mais de 50.000 caracteres são silenciosamente truncados para um preview de 2.000 bytes.

Se qualquer busca ou comando retornar poucos resultados suspeitos: re-execute com escopo mais estreito (diretório único, glob mais restrito).

**Declare quando suspeitar de truncamento.**

## Por que isso importa

O agente não sabe que um resultado foi truncado — ele apenas vê o que foi entregue. Buscas que deveriam retornar 50 arquivos retornam 3, e o agente age como se os 3 fossem todos. Isso produz refactors incompletos e análises incorretas.

## Sinais de possível truncamento

- Busca ampla retorna resultados anormalmente poucos
- grep/glob em diretório grande retorna menos que o esperado
- Output de comando termina abruptamente sem conclusão natural

## Protocolo de verificação

1. Suspeite quando resultados parecem poucos para o escopo da busca
2. Re-execute com escopo reduzido (um diretório de cada vez)
3. Compare contagens entre buscas para detectar divergência
4. Declare explicitamente: "suspeito de truncamento — re-executando com escopo menor"
