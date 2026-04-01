# Verificação Forçada

> Tecnica de Prompting: **Self-Consistency** - Verificacao sistematica multipla ate convergencia

---

## O Problema: Ilusao de Sucesso

Sua ferramenta interna marca gravacoes de arquivo como "sucesso" assim que os bytes atingem o disco. **Isso nao significa que o codigo compila.** Muitos desenvolvedores relatam "Pronto!" apenas para descobrir erros de TypeScript ou ESLint logo em seguida.

### Chain-of-Thought: Por que isso acontece?

1. **Crenaca equivocada**: "O arquivo foi salvo" != "O codigo esta correto"
2. **Falta de feedback loop**: Sem verificacao automatica, erros persistem
3. **Comprometimento insuficiente**: Relatorios de conclusao prematuros

---

## O Mandamento: Verificacao Obrigatoria

**Voce e PROIBIDO de reportar uma tarefa como completa ate executar:**

### Comandos Obrigatorios

```bash
# Verificacao de tipos (obrigatorio se projeto usar TypeScript)
npx tsc --noEmit

# Linting (obrigatorio se ESLint configurado)
npx eslint . --quiet
```

### Ciclo de Feedback Explicito

```
+-----------------+
|   RUN CHECKS    | <-- Inicio: execute os comandos
+--------+--------+
         |
         v
+-----------------+
|   ANY ERRORS?   | <-- Analise output cuidadosamente
+--------+--------+
         |
    +----+----+
    |         |
    v         v
+-------+  +---------+
|  YES  |  |   NO    |
+---+---+  +----+----+
    |           |
    v           v
+-----------+  +---------------+
| FIX ALL   |  | STATE: CLEAN   |
| ERRORS    |  +---------------+
+-----+-----+         |
      |               v
      |        +---------------+
      |        | REPORT DONE   | <-- So agora pode reportar sucesso
      |        +---------------+
      |
      +--------+
               v
        +-------------+
        | REPEAT LOOP | <-- Volte ao inicio, re-execute tudo
        +-------------+
```

### Regra de Ouro

> **Repita o ciclo ate o output estar completamente limpo.** Nao existe "so um warning". Nao existe "vou deixar para depois". Limpo = zero erros.

---

## Template de Verificacao

Antes de declarar "Pronto!", preencha este checklist:

```markdown
## Verification Checklist

- [ ] `npx tsc --noEmit` executado
- [ ] `npx eslint . --quiet` executado (se configurado)
- [ ] Todos os erros de TypeScript corrigidos
- [ ] Todos os erros de ESLint corrigidos
- [ ] Output final: **CLEAN**

### Caso Especial: Sem Type-Checker

Se o projeto nao tem TypeScript configurado:

- [ ] Type-checker: **NAO CONFIGURADO** (explicito)
- [ ] ESLint executado: [SIM/NAO]
- [ ] Estado: [LIMPO/NAO APLICAVEL]

**Importante:** Nunca diga "Pronto!" com erros pendentes. Se nao ha type-checker, declare isso explicitamente em vez de fingir sucesso.
```

---

## Exemplos de Anti-Padroes

### ❌ Errado: Relatorio prematuro

```
Usuario: Crie um componente Button

Claude: [edita 3 arquivos]

Pronto! Criei o componente Button.
```

**Problema**: Nenhuma verificacao foi feita. Pode haver erros de importacao, tipos incorretos, etc.

### ✅ Certo: Verificacao completa

```
Usuario: Crie um componente Button

Claude: [edita 3 arquivos]

[Executando verificacoes...]
- npx tsc --noEmit: 2 erros encontrados
  - src/Button.tsx:15 - Type 'string' is not assignable to type 'ButtonVariant'
  - src/Button.tsx:23 - Cannot find module './styles'

Corrigindo...

[Re-executando...]
- npx tsc --noEmit: CLEAN ✓
- npx eslint . --quiet: CLEAN ✓

Pronto! Componente Button criado e verificado.
```

---

## Self-Consistency em Acao

A tecnica de **Self-Consistency** exige que voce:

1. **Verifique multiplas vezes** - Uma execucao nao basta; re-execute apos correcoes
2. **Seja sistematico** - Mesmo processo sempre, sem excecoes
3. **Converja para zero** - Continue ate nao haver mais erros
4. **Documente o estado** - Declare explicitamente se esta limpo ou nao

> **Lembre-se**: "Seu codigo nao existe ate que compile sem erros."
