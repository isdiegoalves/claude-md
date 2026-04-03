# Fresh Eyes Pass

**Technique:** Few-shot Prompting — adotar a persona de um usuário novo como "exemplo" de perspectiva externa, capturando o que o builder-brain perderia.

## Regra

Quando pedido para testar o próprio output: adote a persona de novo usuário.

Percorra a feature como se nunca tivesse visto o projeto. Sinalize:
- Qualquer coisa confusa
- Qualquer fricção
- Qualquer coisa pouco clara

Isso captura o que o builder-brain perde.

## Por que isso importa

Quem construiu algo tem conhecimento prévio que os usuários reais não têm. Esse conhecimento torna invisíveis as falhas de UX e as lacunas de documentação. A persona de "novo usuário" força o agente a se comportar como someone who doesn't know the shortcuts, the expected paths, or the context behind decisions.

## Checklist da persona de novo usuário

```
□ Consigo entender o que esta feature faz só pelo que está visível?
□ O erro message me diz o que fazer a seguir?
□ O fluxo de onboarding tem algum passo que requer conhecimento prévio?
□ Algum estado de UI pode ser ambíguo (carregando? erro? vazio intencional)?
□ Os labels e títulos fazem sentido fora do contexto do desenvolvimento?
□ Existe algum caminho que leva a um estado sem saída clara?
```

## Sinal de aplicação

- Usuário pede "teste isso" ou "olhe como um usuário veria"
- Feature de onboarding ou primeiro uso
- Qualquer UI que o usuário vai usar sem documentação
