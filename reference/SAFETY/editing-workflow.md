# Edit Integrity

**Technique:** ReAct (Reasoning + Acting) — ciclo explícito de leitura → raciocínio → ação → verificação antes e depois de cada edição.

## Regra

Antes de CADA edição de arquivo: re-leia o arquivo.  
Após editar: leia novamente para confirmar que a mudança foi aplicada corretamente.

O Edit tool falha silenciosamente quando `old_string` não corresponde por contexto antigo.

**Nunca agrupe mais de 3 edits no mesmo arquivo sem uma leitura de verificação.**

## Por que isso importa

O agente opera contra uma representação em memória do arquivo — não contra o arquivo atual. Se o arquivo mudou (por outro agente, pelo usuário, ou pela própria sessão), a old_string não encontra correspondência e a edição silenciosamente não acontece. O agente então reporta sucesso para uma mudança que não ocorreu.

## Protocolo

```
1. Read(arquivo)          ← estado atual garantido
2. Planejar edit
3. Edit(arquivo, ...)     ← aplicar mudança
4. Read(arquivo)          ← verificar que aplicou
5. Repetir (máx 3 vezes antes de nova verificação)
```

## Sinal de aplicação

- Qualquer uso do Edit tool
- Especialmente após qualquer compaction ou mensagem longa
- Quando o arquivo foi tocado na mesma sessão por outra ferramenta
