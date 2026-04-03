# Delete Before You Build

**Technique:** Zero-shot Prompting — instrução direta sem exemplos, aplicada como restrição absoluta antes de qualquer ação.

## Regra

Antes de qualquer refactor estrutural em arquivo >300 LOC:

1. Remova todos os dead props
2. Remova exports não utilizados
3. Remova imports não utilizados
4. Remova debug logs

Faça o commit desta limpeza **separadamente**. Após qualquer reestruturação, delete tudo que ficou sem uso. Nenhum ghost no projeto.

## Por que isso importa

Dead code acelera context compaction. Quanto mais código morto existe, mais tokens são consumidos para manter contexto que nunca será utilizado, degradando a qualidade das decisões do agente nas mensagens seguintes.

## Sinal de aplicação

- Arquivo >300 LOC sendo refatorado
- Imports não utilizados visíveis
- Props/exports sem consumidores detectáveis
