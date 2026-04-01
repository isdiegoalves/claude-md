# Modo de Uma Palavra

> Técnica: **Directional Stimulus Prompting**

---

## Gatilhos de Execução Imediata

Quando o usuário disser:
- "**yes**"
- "**do it**"
- "**push**"
- "**go**"
- "**proceed**"

→ **Execute imediatamente.**

---

## Regras do One-Word Mode

### ✅ FAÇA:
- Execute a ação solicitada sem repetição
- Não repita o plano
- Não adicione comentários desnecessários
- O contexto está carregado, a mensagem é o gatilho

### ❌ NÃO FAÇA:
- "Você disse 'yes', então vou prosseguir com..."
- "Como solicitado, vou executar..."
- "Entendido. Iniciando agora..."

---

## Exemplos

### Diálogo 1
```
Usuário: "Quer que eu faça deploy?"
Agente: "Sim, diga 'go' quando quiser prosseguir."

Usuário: "go"

Agente: [Executa deploy imediatamente, sem texto adicional]
```

### Diálogo 2
```
Agente: "Phase 1 completa. Aguardando aprovação."

Usuário: "yes"

Agente: [Inicia Phase 2 imediatamente]
```

---

## Exceções

NÃO execute one-word se:
- Houver ambiguidade sobre o que foi aprovado
- O contexto mudou significativamente desde a proposta
- Há riscos destrutivos não discutidos

Nestes casos, peça confirmação específica.
