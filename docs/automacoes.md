# Automações

Os três arquivos `.flow-meta.xml` recuperados indicam status `Active`, API `66.0` e processos acionados por registro.

## `Atualizar_Status_do_Estoque`

- Objeto de início: `Product2`.
- Momento: antes de salvar (`RecordBeforeSave`).
- Usa `Estoque_Minimo__c` e atribui valores a `Estatus_de_Estoque__c` para os estados “Baixo Estoque”, “Esgotado” e “Normal”.

## `Flow_Atualizar_Estoque`

- Objeto de início: `Movimentacao_de_estoque__c`.
- Momento: após salvar (`RecordAfterSave`).
- Procura `Product2` por `$Record.Produto__c`.
- Para “Entrada”, soma `$Record.Quantidade__c` a `Quantidade_em_Estoque__c`; para “Saída”, subtrai essa quantidade.

## `Alerta_de_Estoque_Baixo`

- Objeto de início: `Product2`.
- Momento: após salvar (`RecordAfterSave`).
- Verifica `Estatus_de_Estoque__c` e, na condição de baixo estoque, cria uma `Task` associada ao produto (`WhatId`) e atribuída ao usuário atual (`$User.Id`). Os metadados definem assunto, descrição, prioridade e status da tarefa.

## Regra de validação

`Movimentacao_de_estoque__c.Bloquear_Saida_Maior_Que_Estoque` está ativa. Para `Saída`, impede quantidade maior que `Produto__r.Quantidade_em_Estoque__c`.

## Dependências observadas

`Product2`, `Movimentacao_de_estoque__c`, `Task`, `$User` e os campos citados. A movimentação consulta `Product2` por `Produto__c`. Não foram encontradas referências a Apex ou subflows nestes três arquivos. Esta documentação descreve o XML recuperado; não afirma que os Flows foram executados ou testados.
