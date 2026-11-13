# NutriStock

Aplicativo Salesforce para registrar produtos, lotes e movimentações de estoque. Este repositório reúne uma recuperação seletiva de metadados Salesforce e a conversão para o formato Salesforce DX. A documentação descreve somente componentes confirmados nos metadados recuperados.

## Recursos confirmados

- Aplicativo Lightning `NutriStock`, com navegação para produtos, contas, contatos, lotes e movimentações.
- Cadastro de produtos em `Product2`, com categoria, marca, custo, preço de venda, estoque mínimo, quantidade e status de estoque.
- Objetos personalizados para fornecedores, lotes e movimentações, com layouts e listas relacionados.
- Página de registro para `Product2` e utility bar do aplicativo.
- Traduções `pt_BR` para os três objetos personalizados.
- Regra de validação que impede registrar uma saída acima do estoque disponível.
- Três Flows para atualizar status do estoque, calcular movimentações e criar tarefa de reposição quando um produto está com baixo estoque.

## Tecnologias

- Salesforce Platform e Salesforce DX
- Metadados Metadata API convertidos para source format
- Lightning App, Lightning Record Page, layouts e abas
- Salesforce Flow e regras de validação
- XML de metadados; versão de API definida no projeto: `66.0`

Não foram recuperadas classes Apex nem componentes Lightning Web Components para este aplicativo.

## Modelo de dados

- `Product2`: produto e saldo de estoque, incluindo `Quantidade_em_Estoque__c` e `Estoque_Minimo__c`.
- `Fornecedor__c`: dados cadastrais do fornecedor.
- `Lote_do_Produto__c`: validade, quantidade e status do lote; `Produto__c` referencia `Product2`.
- `Movimentacao_de_estoque__c`: tipo, quantidade, data e motivo da movimentação; `Produto__c` referencia `Product2`.
- O campo `Movimentacao_de_estoque__c.Fornecedor__c` referencia `Account`, não `Fornecedor__c`. O relacionamento foi preservado como recuperado.

Veja [docs/modelo-de-dados.md](docs/modelo-de-dados.md) para os campos e relações confirmados.

## Automações

1. `Atualizar_Status_do_Estoque` define o estado do estoque de `Product2` antes de salvar.
2. `Flow_Atualizar_Estoque` soma entradas ou subtrai saídas no saldo do produto após salvar uma movimentação.
3. `Alerta_de_Estoque_Baixo` cria uma tarefa de reposição associada ao produto.
4. `Bloquear_Saida_Maior_Que_Estoque` valida a quantidade de uma saída contra o saldo atual.

Consulte [docs/automacoes.md](docs/automacoes.md) para as referências observadas nos metadados.

## Estrutura

```text
force-app/main/default/   Metadados Salesforce DX
manifest/package.xml      Manifesto seletivo usado na recuperação
scripts/                  Exemplos padrão gerados pelo template Salesforce DX
config/                   Configuração scratch org gerada pelo template
docs/                    Documentação técnica do projeto
```

Os exemplos genéricos de Apex anônimo e consulta SOQL criados pelo template foram removidos; não faziam parte dos metadados do NutriStock.

## Limitações conhecidas

A recuperação não inclui o asset de logo `ContentAsset nutri_stock` nem a Lightning Page `Conta_P_gina_de_registro`, ambos referenciados pela configuração do aplicativo. Relatórios, dashboards e permissões não fazem parte do pacote recuperado. A ausência desses itens no pacote não confirma que não existam na organização. Veja [docs/recuperacao-e-lacunas.md](docs/recuperacao-e-lacunas.md).

## Segurança e publicação

O `.gitignore` exclui caches Salesforce, credenciais locais, arquivos temporários, dados tabulares e a pasta `recovery/`. Revise toda alteração antes de publicar; não inclua dados reais, tokens ou arquivos de autenticação.

## Documentação

- [Arquitetura](docs/arquitetura.md)
- [Modelo de dados](docs/modelo-de-dados.md)
- [Automações](docs/automacoes.md)
- [Recuperação e lacunas](docs/recuperacao-e-lacunas.md)


