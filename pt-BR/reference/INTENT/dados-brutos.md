# Trabalhe com Dados Brutos

> Técnica: **Zero-shot Prompting**

---

## O Princípio

Quando o usuário colar logs de erro, trabalhe **diretamente com aqueles dados**.

❌ **NÃO:**
- Adivinhe a causa
- Persiga teorias
- Ignore o erro real

✅ **SIM:**
- Trace o erro exato nos dados fornecidos
- Use linha/column do stack trace
- Leia o código na posição exata indicada

---

## Checklist de Debugging com Dados Brutos

### Recebendo um Report de Bug
- [ ] Leia o stack trace completo
- [ ] Identifique arquivo e linha exata do erro
- [ ] Leia o código nessa linha específica
- [ ] Entenda o estado das variáveis no momento do erro
- [ ] NÃO faça suposições sobre causas

### Solicitando Mais Informação
```
Se o bug report não tiver error output:
"Cole a saída do console — dados brutos encontram
o problema real mais rápido."
```

---

## Exemplo de Fluxo Correto

**Bug Report:**
```
TypeError: Cannot read property 'name' of undefined
    at UserProfile.render (UserProfile.tsx:42)
    at ReactDOM.render (react-dom.js:123)
```

❌ **ERRADO:**
"Parece ser um problema com o componente UserProfile.
Vou verificar os props..."

✅ **CORRETO:**
```
Analisando erro em UserProfile.tsx:42...

Lendo linha 42:
  return <div>{user.name}</div>;

Observação: 'user' está undefined neste ponto.

Verificando de onde vem 'user'...
[Investigação baseada no código real]
```

---

## Anti-Patterns

| Anti-Pattern | Por que é ruim? | Solução |
|--------------|-----------------|---------|
| "Parece ser..." | Suposição sem dados | Sempre verifique o código exato |
| "Provavelmente..." | Teoria sem confirmação | Trace o erro passo a passo |
| "Talvez seja X" | Chute | Leia os dados, não adivinhe |
| Ignorar stack trace | Perde informação preciosa | Use linha:coluna fornecida |
