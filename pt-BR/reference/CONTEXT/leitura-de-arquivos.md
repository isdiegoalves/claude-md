# Orçamento de Leitura de Arquivos

> Técnica: **Zero-shot Prompting** | Source: CLAUDE.md §4

---

## Limites Fundamentais

```
+----------------------------------------+
|  MÁXIMO POR READ: 2,000 linhas       |
|  (= ~167K tokens de contexto)        |
+----------------------------------------+
```

**Nunca assuma** que viu o arquivo completo em uma única leitura se:
- Arquivo tem >500 LOC (Lines of Code)
- Mensagem de erro truncada
- Resultado parece incompleto

---

## Uso de Offset e Limit

### Sintaxe Básica

```typescript
Read({
  file_path: "/abs/path/to/file.ts",
  offset: 1,      // Linha inicial (1-based)
  limit: 500      // Quantidade de linhas
})
```

### Padrão de Navegação

```
Leitura 1: offset=1,   limit=500  → Linhas 1-500
Leitura 2: offset=501, limit=500  → Linhas 501-1000
Leitura 3: offset=1001, limit=500 → Linhas 1001-1500
Leitura 4: offset=1501, limit=500 → Linhas 1501-2000
...e assim por diante
```

---

## Estratégias para Arquivos >500 LOC

### Estratégia 1: Busca Direcionada (Recomendada)

**Quando usar:** Você sabe o que procura

1. Use `Grep` para localizar padrões específicos
2. Leia apenas as seções relevantes com offset/limit
3. Navegue por referências (imports, exports)

```typescript
// Passo 1: Encontrar onde está a função
Grep({ pattern: "function handleAuth", path: "/src" })

// Passo 2: Ler apenas o bloco relevante
Read({ file_path: "/src/auth/handlers.ts", offset: 145, limit: 50 })
```

### Estratégia 2: Leitura Sequencial em Chunks

**Quando usar:** Precisa entender o arquivo inteiro

```
Chunk 1: Cabeçalho e imports (offset 1, limit 50)
Chunk 2: Interfaces e tipos (offset 51, limit 100)
Chunk 3: Funções principais (offset 151, limit 300)
Chunk 4: Helpers e utils (offset 451, limit 200)
...
```

---

## Checklist de Leitura

### Antes de Ler
- [ ] Estime o tamanho do arquivo
- [ ] Defina objetivo claro da leitura
- [ ] Escolha estratégia apropriada

### Durante a Leitura
- [ ] Se >500 LOC: use offset/limit
- [ ] Anote linhas de interesse para re-leitura
- [ ] Verifique imports/exports para navegação

### Após Ler
- [ ] Confirme que viu seções necessárias
- [ ] Navegue para arquivos referenciados se necessário
- [ ] Valide suposições com segunda leitura se incerto
