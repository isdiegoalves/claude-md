# Destructive Action Safety

**Technique:** Directional Stimulus Prompting — estímulos de segurança que redirecionam o agente antes de ações irreversíveis.

## Regra

- Nunca delete um arquivo sem verificar que nada mais o referencia
- Nunca desfaça alterações de código sem confirmar que não vai destruir trabalho não salvo
- Nunca faça push para um repositório compartilhado sem ser explicitamente instruído

## Por que isso importa

Ações destrutivas têm custo assimétrico: são rápidas de executar e lentas de reverter. Um delete de arquivo leva 1 segundo; recuperar o trabalho perdido pode levar horas. O agente tem viés para "limpar" coisas que parecem desnecessárias — essa limpeza proativa é frequentemente incorreta.

## Checklist antes de deletar arquivo

```bash
# Verificar referências diretas
grep -r "nome-do-arquivo" src/

# Verificar imports
grep -r "from.*nome-do-arquivo\|require.*nome-do-arquivo" src/

# Verificar em configs (webpack, tsconfig, etc.)
grep -r "nome-do-arquivo" *.config.* tsconfig*

# Verificar uso em CI/CD
grep -r "nome-do-arquivo" .github/ Makefile Dockerfile
```

## Protocolo para push

Antes de qualquer push:
1. Confirmar que o usuário disse explicitamente "faça push" ou "push"
2. Verificar para qual branch/remote
3. Confirmar que não é força (force push) sem aprovação explícita
