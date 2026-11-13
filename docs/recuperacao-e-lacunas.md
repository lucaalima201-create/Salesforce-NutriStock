# Recuperação e lacunas

## Escopo recuperado

O manifesto seletivo contém 12 tipos e 53 membros. O manifesto da recuperação foi comparado ao manifesto seletivo: os membros coincidiram. A conversão gerou metadados Salesforce DX sob `force-app/main/default`, incluindo aplicativo, objetos, campos, listas, regra de validação, Flows, definições de Flow, layouts, abas, traduções e FlexiPages.

O projeto DX contém 24 campos personalizados do pacote. O objeto padrão `Product2` também converteu campos padrão presentes no metadata de origem; esses itens não devem ser confundidos com campos customizados do NutriStock.

## Dependências pendentes

- **`ContentAsset nutri_stock`**: a aplicação referencia este logo, mas o asset não foi recuperado.
- **`FlexiPage Conta_P_gina_de_registro`**: a aplicação contém referência a esta página, mas ela não foi recuperada.

Não foram criados placeholders nem substitutos para essas dependências.

## Componentes fora do pacote

O pacote não contém relatórios, dashboards, permission sets, perfis, Apex, LWC ou `StaticResource`. Essa ausência é uma limitação do escopo recuperado, não prova de inexistência na organização.

A navegação da aplicação declara `Product2`, `Account`, `Contact`, `Movimentacao_de_estoque__c` e `Lote_do_Produto__c`. A aba `Fornecedor__c` foi recuperada, mas não aparece na lista de navegação do aplicativo.

## Relacionamento de fornecedor

O campo `Movimentacao_de_estoque__c.Fornecedor__c` aponta para `Account`. O projeto também contém o objeto separado `Fornecedor__c`, mas os metadados não conectam esse objeto ao campo de movimentação. O relacionamento foi preservado e não foi corrigido automaticamente.

## Arquivos de template

Os exemplos genéricos `scripts/apex/hello.apex` e `scripts/soql/account.soql` do template Salesforce DX foram removidos após confirmação de que não tinham dependências fora desta documentação. As configurações padrão de lint, Jest, Husky, VS Code e scratch org também vieram da estrutura gerada e não são componentes funcionais recuperados. Nenhum teste foi executado nesta preparação.

## Origem e limitações da recuperação

O material original veio de uma recuperação Metadata API seletiva. O ZIP esperado não foi encontrado na pasta declarada anteriormente; a árvore extraída estava em `unpackaged/unpackaged`. Para detalhes de dependências, consulte o `manifest/package.xml` e os metadados em `force-app/main/default`.

## Revisão para publicação

Foi feita uma busca textual por padrões comuns de senhas, tokens, chaves privadas e credenciais embutidas; não houve correspondências nos arquivos existentes durante a revisão. Essa busca não substitui revisão manual. Não publique tokens, arquivos de autenticação, dados de registros, exports CSV ou credenciais de ambiente.

A pasta `recovery/`, caches, artefatos temporários, arquivos de autenticação e dados tabulares estão excluídos pelo `.gitignore` deste projeto.

## Estado Git observado

O diretório possui um repositório Git próprio, com raiz `C:/Users/dell/Projetos-DevHero/Salesforce-NutriStock`, na branch `main`. Na data desta revisão não havia commits. O repositório pai `C:/Users/dell/Projetos-DevHero` não rastreia os arquivos internos; evite adicionar a pasta aninhada pelo repositório pai. Não foi feito commit nem push.


