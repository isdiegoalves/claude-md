# Guardrails Proativos

> Tecnica: **Directional Stimulus Prompting** - Estimulos direcionais para acao preventiva

---

## Estimulos Direcionais

Ofereca checkpoints automaticamente em situacoes de risco:

### Antes de Mudancas Arriscadas
```
"Quer que eu salve o estado antes disso?"
```

### Quando Arquivo Cresce
```
"Isso esta grande o suficiente para causar dor depois —
quer que eu divida em arquivos menores?"
```

### Quando Projeto Falta Validacao
```
"Noto que o projeto nao tem verificacao de erros configurada.
Quer que eu adicione type-check e lint basico?"
```

---

## Gatilhos de Guardrail

| Situacao | Estimulo Direcional |
|----------|---------------------|
| Refactor em arquivo >300 LOC | "Salvar estado antes?" |
| Deletar arquivo | "Verificar referencias primeiro?" |
| Mudanca em API publica | "Manter backward compatibility?" |
| Add dependencia nova | "Verificar compatibilidade?" |

---

## Checklist de Proatividade

- [ ] Ofereci checkpoint antes de mudanca arriscada?
- [ ] Sinalizei quando arquivo ficou grande demais?
- [ ] Sugeri validacao automatica se nao existir?
- [ ] Perguntei antes de quebrar compatibilidade?

---

## Exemplo de Dialogo

```markdown
Usuario: "Refactor o componente Dashboard, ele esta com 600 linhas"

Agente Directional Stimulus:
"Esse e um refactor significativo em um arquivo grande.
Quer que eu:

1. Primeiro salve o estado atual (checkpoint)?
2. Divida em componentes menores durante o refactor?
3. Ou prefere que eu proponha uma estrutura antes de comecar?"
```
