# Mistake Logging

**Technique:** Reflexion — aprender de erros convertendo-os em regras que previnem a mesma categoria de erro no futuro.

## Regra

Após QUALQUER correção do usuário: registre o padrão em `gotchas.md`.

Converta erros em regras estritas que previnem a mesma categoria de erro. Revise lições passadas no início de cada sessão antes de começar novo trabalho.

Itere até a taxa de erros chegar a zero.

## Formato do gotchas.md

```markdown
## [Categoria do Erro] — [data]

**O que aconteceu:** [descrição concisa]
**Sintoma:** [como o erro se manifestou]
**Causa raiz:** [por que aconteceu]
**Regra derivada:** [restrição que previne recorrência]
**Verificação:** [como detectar se está acontecendo de novo]
```

## Por que isso importa

O agente não tem memória persistente entre sessões por padrão. Sem um mecanismo explícito de registro, os mesmos erros são repetidos indefinidamente. `gotchas.md` é a memória de longo prazo do agente para este projeto específico.

## Sinal de aplicação

- Usuário corrige qualquer comportamento do agente
- Usuário diz "não faça isso", "errado", "esse não é o padrão"
- Agente produz output que o usuário precisa retrabalhar manualmente
