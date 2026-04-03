# File Read Budget

**Technique:** Zero-shot Prompting — restrição direta que previne suposição silenciosa de completude.

## Regra

Cada leitura de arquivo está limitada a 2.000 linhas. Para arquivos com mais de 500 LOC:

- DEVE usar parâmetros `offset` e `limit` para ler em chunks sequenciais
- Nunca assuma ter visto um arquivo completo a partir de uma única leitura

## Por que isso importa

O agente não recebe aviso quando uma leitura é truncada — ela simplesmente para. A suposição silenciosa de "li o arquivo inteiro" leva a edits que ignoram código abaixo do corte, quebrando lógica que existia mas não foi vista.

## Protocolo para arquivos grandes

```
Leitura 1: offset=0, limit=500    → linhas 1-500
Leitura 2: offset=500, limit=500  → linhas 501-1000
Leitura 3: offset=1000, limit=500 → linhas 1001-1500
...continue até não haver mais conteúdo
```

## Sinal de aplicação

- Arquivo que retorna exatamente 2.000 linhas (suspeita de truncamento)
- Edição em arquivo cujo tamanho é desconhecido
- Busca por função que não foi encontrada (pode estar abaixo do corte)
