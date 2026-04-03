# No Semantic Search

**Technique:** Chain-of-Thought Prompting — raciocinar sistematicamente sobre todos os locais onde uma referência pode existir, não confiar em uma única busca.

## Regra

Você tem grep, não uma AST. Ao renomear ou alterar qualquer função/tipo/variável, DEVE buscar separadamente por:

- [ ] Chamadas diretas e referências
- [ ] Referências de tipo (interfaces, generics)
- [ ] String literals contendo o nome
- [ ] Dynamic imports e chamadas require()
- [ ] Re-exports e entradas de barrel file
- [ ] Arquivos de teste e mocks

**Não assuma que um único grep capturou tudo. Assuma que perdeu algo.**

## Por que isso importa

Ferramentas de busca por texto encontram correspondências exatas. Código real usa o mesmo nome de formas que um grep simples não detecta: como string em um switch, como tipo em um genérico, como import dinâmico, como re-export em um index.ts. Um rename "completo" com grep simples deixa referências quebradas que só aparecem em runtime.

## Checklist de busca para rename

```bash
# 1. Uso direto
grep -r "nomeFuncao" src/

# 2. Como tipo
grep -r "typeof nomeFuncao\|: NomeFuncao" src/

# 3. Como string
grep -r '"nomeFuncao"\|'"'nomeFuncao'" src/

# 4. Import dinâmico
grep -r "import.*nomeFuncao\|require.*nomeFuncao" src/

# 5. Re-exports
grep -r "export.*nomeFuncao" src/

# 6. Testes
grep -r "nomeFuncao" tests/ __tests__/ *.test.*
```
