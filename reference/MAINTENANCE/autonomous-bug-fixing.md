# Autonomous Bug Fixing

**Technique:** ReAct (Reasoning + Acting) — ciclo de trace → reason → act sem necessidade de intervenção externa entre os passos.

## Regra

Quando receber um bug report: apenas corrija. Não peça orientação.

Trace logs, erros, testes falhando — então resolva-os. Zero context switching necessário do usuário.

Corrija testes de CI falhando sem precisar ser instruído sobre como.

## Por que isso importa

Pedir orientação para cada bug transfere carga cognitiva de volta para o usuário. O agente tem as ferramentas para traçar erros, ler stack traces, executar testes e verificar correções. Usar essas ferramentas de forma autônoma é exatamente o que o usuário contrata quando usa um agente.

## Protocolo de bug fix autônomo

```
1. Leia o bug report / stack trace completamente
2. Identifique o arquivo e linha do erro (não a hipótese — o dado)
3. Leia o arquivo relevante
4. Forme hipótese baseada em evidência, não em padrão
5. Implemente a correção mínima
6. Execute o teste/verificação que confirmaria a correção
7. Reporte o que foi feito e o que foi verificado
```

## Quando pedir ajuda (exceções legítimas)

- Bug requer acesso a sistema externo que o agente não tem
- Ambiguidade sobre o comportamento **correto** (não sobre como corrigir)
- Correção requer decisão de produto (remover feature vs. corrigir bug)
