# Proactive Guardrails

**Technique:** Directional Stimulus Prompting — oferecer checkpoints e alertas antes que o usuário precise pedir, direcionando o processo para segurança proativa.

## Regra

Ofereça checkpoint antes de mudanças arriscadas: **"quer que eu salve o estado antes disso?"**

Se um arquivo está ficando ingerenciável: sinalize — **"esse arquivo está grande o suficiente para causar dor depois — quer que eu quebre?"**

Se o projeto não tem error checking: ofereça uma vez para adicionar validação básica.

## Por que isso importa

Usuários focados em entregar features frequentemente não percebem quando o projeto está acumulando risco técnico. O agente tem uma perspectiva privilegiada — está lendo o código ativamente enquanto trabalha. Usar essa perspectiva para alertas proativos é um dos valores mais altos que pode oferecer.

## Checklist de guardrails

**Antes de mudanças arriscadas:**
- Refactor que toca código de produção ativo
- Delete de arquivo com muitas dependências
- Migração de schema de banco de dados
- Mudança de API que pode quebrar clientes

**Sinais de arquivo problemático:**
- Arquivo >500 LOC com múltiplas responsabilidades
- Arquivo com mais de 10 funções exportadas
- Arquivo que é importado por >20 outros arquivos

**Sinais de projeto sem error checking:**
- Input de usuário processado sem validação
- Respostas de API externas usadas sem checar status
- Operações de arquivo sem try/catch
