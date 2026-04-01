# Planejar e Construir São Passos Separados

**Padrão:** Chain-of-Thought Prompting
**Fonte:** CLAUDE.md Seção 1 - Pré-Trabalho

> Quando pedido para "fazer um plano" ou "pensar nisso primeiro", produza apenas o plano. Sem código até o usuário dizer "vá". Quando o usuário fornecer um plano por escrito, siga-o exatamente. Se você identificar um problema real, sinalize e aguarde — não improvise. Se as instruções forem vagas (ex: "adicione uma página de configurações"), não comece a construir. Descreva o que você construiria e onde isso iria. Obtenha aprovação primeiro.

---

## Quando Outputar Apenas o Plano

### Gatilhos de Modo Plano

| Solicitacao do Usuario | Acao | Exemplo |
|------------------------|------|---------|
| "make a plan" | Apenas plano, sem codigo | Output estrutura do plano |
| "think about this first" | Apenas plano, sem codigo | Analise e recomendacoes |
| "how would you approach..." | Apenas plano, sem codigo | Estrategia e trade-offs |
| "outline..." | Apenas plano, sem codigo | Estrutura de implementacao |

### Resposta Padrao para Modo Plano

```markdown
## Plano: [Nome da Tarefa]

### Visao Geral
[Breve descricao do que sera construido]

### Estrutura Proposta

#### Arquivos a Criar
1. `path/to/file1.ts` - [Responsabilidade]
2. `path/to/file2.ts` - [Responsabilidade]
3. `path/to/file3.ts` - [Responsabilidade]

#### Arquivos a Modificar
1. `path/to/existing1.ts` - [Mudanca necessaria]
2. `path/to/existing2.ts` - [Mudanca necessaria]

### Dependencias
- [Lista de dependencias externas necessarias]

### Potenciais Problemas
- [Identificar problemas conhecidos]

### Proximos Passos
Aguardando sua confirmacao com "yes", "go", ou "do it" para iniciar implementacao.
```

---

## Quando Esperar Aprovacao

### Cenarios que Requerem Aprovacao Explicita

| Cenario | Por que Esperar? | Exemplo de Input Vago |
|---------|------------------|----------------------|
| **Instrucoes vagas** | Sem especificacao clara de comportamento | "add a settings page" |
| **Escopo indefinido** | Nao esta claro o que deve ser incluido | "melhorar o dashboard" |
| **Multiplas opcoes** | Mais de uma abordagem valida | "refactor do auth" |
| **Alto impacto** | Mudancas que afetam muitos arquivos | "migrar para nova arquitetura" |
| **Ambiguidade** | Pode ser interpretado de varias formas | "adicionar suporte a themes" |

### O Que Obter Antes de Construir

1. **Especificacao clara**: O que exatamente deve ser feito
2. **Escopo definido**: Limites do que esta incluido/nao incluido
3. **Abordagem confirmada**: Qual solucao adotar
4. **Aprovacao explicita**: "yes", "go", "do it", "proceed"

---

## Como Lidar com Instrucoes Vagas

### Exemplo: "Add a settings page"

```
❌ Errado: Comecar a codar imediatamente
✅ Correto:
   1. Fazer perguntas clarificadoras:
      - "Quais configuracoes devem estar disponiveis?"
      - "Deve ser uma pagina separada ou modal?"
      - "Ha design/mockup existente para seguir?"
      - "Onde deve estar o link de acesso?"
   2. Apresentar outline do que sera construido
   3. Aguardar aprovacao antes de comecar
```

### Template de Resposta para Instrucoes Vagas

```markdown
Antes de comecar, preciso clarificar alguns pontos sobre "[instrucao vaga]":

## Perguntas de Clarificacao

1. [Pergunta especifica sobre comportamento]
2. [Pergunta especifica sobre escopo]
3. [Pergunta especifica sobre design/padroes]

## Proposta Preliminar

Baseado no que entendi, planejo:

### O que construirei:
- [Item 1]
- [Item 2]
- [Item 3]

### Onde ficara:
- `src/path/file1.ts`
- `src/path/file2.ts`

### O que NAO incluirei (a menos que especificado):
- [Escopo fora do obvio]

Por favor, confirme se esta correto ou ajuste o que for necessario.
Diga "go" quando estiver pronto para prosseguir.
```

---

## Regras de Seguir Planos Exatos

### Quando o Usuario Fornece um Plano Escrito

1. **Siga exatamente**: Implemente conforme especificado
2. **Nao improvise**: Nao adicione "melhorias" nao solicitadas
3. **Flag problemas reais**: Se encontrar um problema, reporte e aguarde
4. **Nao contorne**: Nao ignore partes do plano sem aprovacao

### Exemplo de Problema Real

```
Usuario: "Mova a funcao calculateTotal para utils.ts e delete o arquivo
          original sem verificar dependencias"

Agente: Identifiquei um problema: calculateTotal e importado por 5 outros
        arquivos. Deletar sem atualizar os imports quebrara o codigo.

        Opcoes:
        1. Mover e atualizar todos os imports automaticamente
        2. Mover, manter export redirect no arquivo original temporariamente
        3. Reconsiderar a mudanca

        Como deseja proceder?
```

---

## Fluxo de Decisao

```text
+-------------------------------------------------------------+
|  SOLICITACAO DO USUARIO                                     |
+-------------------------------------------------------------+
                              |
                              v
                    +------------------+
                    |  E para fazer    |
                    |  um plano?       |
                    +------------------+
                              |
              +---------------+---------------+
              | SIM                          | NAO
              v                              v
+----------------------------+   +----------------------------+
|  OUTPUT APENAS O PLANO     |   |  Instrucoes sao claras    |
|  • Estrutura               |   |  e especificas?           |
|  • Arquivos                |   +----------------------------+
|  • Trade-offs              |                  |
|  • Sem codigo              |         +-------+-------+
+----------------------------+         | SIM           | NAO
           |                         v               v
           |          +--------------------+  +--------------------+
           |          |  EXECUTAR DIRETO   |  |  INSTRUCOES VAGAS |
           |          |  Seguir plano do   |  |  • Fazer perguntas|
           |          |  usuario exatamente|  |  • Apresentar     |
           |          +--------------------+  |    outline        |
           |                                  |  • Aguardar       |
           |                                  |    aprovacao      |
           |                                  +--------------------+
           |
           v
+----------------------------+
|  AGUARDAR APROVACAO:       |
|  "yes", "go", "do it"      |
+------------------------------------+
           |
           v
+----------------------------+
|  SOMENTE ENTAO:            |
|  INICIAR IMPLEMENTACAO     |
+----------------------------+
```

---

## Prompt Template para Agentes

Use este prompt para instruir qualquer agente sobre este workflow:

```markdown
## Chain-of-Thought: Planejar e Construir Sao Passos Separados

Regras de planejamento:

1. Quando solicitado para "make a plan" ou "think about this first",
   output APENAS o plano - nenhum codigo
2. Quando o usuario fornecer um plano escrito, siga-o exatamente
3. Se encontrar problemas reais, flag e aguarde - nao improvise
4. Para instrucoes vagas (ex: "add a settings page"):
   - Apresente um outline do que construira
   - Especifique onde cada arquivo ficara
   - Aguarde aprovacao explicita antes de comecar

Separacao clara: Plano primeiro, build depois do "go".
```
