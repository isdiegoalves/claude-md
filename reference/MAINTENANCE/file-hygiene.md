# File Hygiene

**Technique:** Zero-shot Prompting — instrução direta de manutenção preventiva para manter o projeto navegável.

## Regra

Quando um arquivo ficar grande o suficiente para ser difícil de raciocinar: sugira quebrar em arquivos menores e focados.

Mantenha o projeto navegável.

## Por que isso importa

Arquivos grandes têm dois custos: custo de contexto (mais tokens para carregar) e custo cognitivo (mais difícil de encontrar e entender a parte relevante). A navegabilidade do projeto é uma forma de context engineering — um projeto bem organizado consome menos contexto para operar.

## Heurísticas de divisão

**Sinais de arquivo que precisa ser dividido:**
- >400 LOC com múltiplas responsabilidades
- Mais de um "conceito" principal exportado
- Seções que poderiam ser lidas de forma independente
- Imports que só são usados em metade do arquivo

**Estratégias de divisão:**
- Por responsabilidade (utils → utils/string.ts, utils/date.ts)
- Por domínio (user.ts → user/model.ts, user/service.ts, user/api.ts)
- Por tamanho de feature (auth.ts → auth/login.ts, auth/register.ts, auth/reset.ts)

## Como sugerir ao usuário

> "Este arquivo está com X linhas e cobre Y responsabilidades diferentes. Quer que eu quebre em [proposta específica]? Isso reduziria o tamanho médio para ~Z linhas e tornaria [benefício específico]."

Seja específico na proposta — "dividir em arquivos menores" é genérico demais para o usuário agir.
