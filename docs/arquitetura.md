# Arquitetura

## Visão geral

O projeto contém o aplicativo Lightning `NutriStock` e metadados declarativos convertidos ao formato Salesforce DX em `force-app/main/default`. Os metadados observados incluem objetos, campos, layouts, listas, abas, páginas Lightning, traduções, Flows e uma regra de validação. Não há código Apex nem LWC recuperados.

## Navegação do aplicativo

`NutriStock.app-meta.xml` declara abas para `Product2`, `Account`, `Contact`, `Movimentacao_de_estoque__c` e `Lote_do_Produto__c`. A utility bar usa `NutriStock_UtilityBar`. Há uma aba recuperada para `Fornecedor__c`, mas ela não consta da navegação declarada do aplicativo.

A aplicação contém referências a `ContentAsset nutri_stock` (logo) e à página `Conta_P_gina_de_registro`; esses componentes não estão no pacote convertido. Eles estão registrados como dependências pendentes, sem criação de substitutos.

## Componentes

| Camada | Componentes confirmados |
|---|---|
| Aplicação | `NutriStock` |
| Dados | `Product2`, `Fornecedor__c`, `Lote_do_Produto__c`, `Movimentacao_de_estoque__c` |
| Interface | 3 layouts, 3 listas, 3 abas personalizadas e 2 FlexiPages |
| Automação | 3 Flows e 1 regra de validação |
| Localização | Traduções `pt_BR` dos 3 objetos personalizados e de seus campos traduzidos |

## Dependências e limites

Os metadados usam objetos padrão `Product2`, `Account`, `Contact` e `Task`. O campo `Movimentacao_de_estoque__c.Fornecedor__c` é lookup para `Account`; não existe no pacote uma referência desse campo para o objeto personalizado `Fornecedor__c`. Essa relação foi mantida sem alteração.

Não há relatórios, dashboards, permission sets, perfis, Apex, LWC ou recursos estáticos no pacote convertido. Não se conclui que estejam ausentes da organização; apenas não foram recuperados neste escopo.
