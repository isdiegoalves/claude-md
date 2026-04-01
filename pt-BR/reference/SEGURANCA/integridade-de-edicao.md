# Integridade de Edição

> Técnica: **ReAct** (Reasoning + Acting)

---

## ReAct Checklist (Copiável)

Use este checklist em cada ciclo de edição:

```
[ ] PASSO 1 - REASON: Por que estou editando este arquivo?
    → Identifique a mudança necessária e o motivo

[ ] PASSO 2 - RE-READ: Ler o arquivo ANTES de editar
    → Confirme: linha X, coluna Y, contexto Z está correto?
    → Responda: Sim/Não - se Não, re-avalie

[ ] PASSO 3 - ACT: Execute a edição com old_string preciso
    → old_string deve ser EXATO (incluindo espaços, quebras de linha)

[ ] PASSO 4 - VERIFY: Leia o arquivo novamente APÓS editar
    → Confirme: a mudança foi aplicada corretamente?
    → Responda: Sim/Não - se Não, investigue falha silenciosa

[ ] PASSO 5 - DECISION: Próximo passo
    → Se 3+ edições neste arquivo → RE-READ obrigatório antes de continuar
    → Se menos de 3 edições → pode continuar (mas preferencialmente verifique)
```

---

## Regra das 3 Edições

**Nunca batch mais de 3 edições sem verificação de leitura.**

| Edições | Ação Obrigatória |
|---------|------------------|
| 1ª      | Re-read após editar (boas práticas) |
| 2ª      | Re-read após editar (boas práticas) |
| 3ª      | **RE-READ OBRIGATÓRIO** antes de 4ª edição |
| 4ª+     | Re-read entre CADA edição subsequente |

---

## Como Detectar Falhas Silenciosas

O Edit tool **falha silenciosamente** quando `old_string` não corresponde.

| Sintoma | Causa Provável | Solução |
|---------|----------------|---------|
| Arquivo parece não mudar | `old_string` com espaços/errados | Re-ler arquivo, copiar texto exato |
| Edit reporta sucesso mas nada muda | Contexto stale | Re-ler arquivo do zero |
| old_string "não encontrado" | Quebras de linha diferentes | Usar editor para visualizar whitespace |
| Mudança parcial aplicada | `old_string` corresponde parcialmente | Verificar se há múltiplas ocorrências |

---

## Exemplo de Aplicação ReAct

**Cenário:** Renomear função `handleClick` para `handleSubmit`

```
Thought: Preciso renomear handleClick em components/Button.tsx
         Vai afetar exports e props.

Action: Read file /project/components/Button.tsx

Observation:
- Line 15: export function handleClick() {
- Line 42: onClick={handleClick}
- Line 89: const handleClick = useCallback(...)

Thought: 3 ocorrências. A última é uma variável local.
         Preciso mudar nome da função exportada.

Action: Edit file com old_string="export function handleClick()"

Observation (after edit):
- Line 15: export function handleSubmit() {
- Line 42: onClick={handleClick}  // <- ainda referencia nome antigo

Thought: Falha parcial! A referência na linha 42 não foi atualizada.
          Preciso de mais uma edição.

Action: Edit file com old_string="onClick={handleClick}"

Observation (after edit):
- Line 42: onClick={handleSubmit}

Thought: Verificação completa. 2 edições feitas. < 3, posso continuar.
         Mas vou fazer verify read para garantir.

Action: Read file novamente para confirmar ambas mudanças
```
