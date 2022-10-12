# **Synapse Analytics Trainning**
Synapse Training - Based on Microsoft learn

https://learn.microsoft.com/pt-br/azure/synapse-analytics/get-started


Siga as etapas na ordem mostrada abaixo e você fará um tour por muitas funcionalidades e aprenderá a exercitar os principais recursos.

- ETAPA 1 – Criar e configurar um workspace do Synapse
- ETAPA 2: Análise por meio de um pool de SQL sem servidor
- ETAPA 3 – Analisar usando um pool do Data Explorer
- ETAPA 4 – Analisar usando o Apache Spark
- ETAPA 5 – Analisar por meio de um pool de SQL dedicado
- ETAPA 6 – Analisar dados em uma conta de armazenamento
- ETAPA 7 – Orquestrar com pipelines
- ETAPA 8 – Visualizar dados com o Power BI
- ETAPA 9 – Monitorar atividades
- ETAPA 10 – Explorar o Centro de Conhecimento
- ETAPA 11 – Adicionar um administrador

---

# Como criar um workspace do Azure Synapse

Neste tutorial, você aprenderá a criar um workspace do Azure Synapse, um pool de SQL dedicado e um Pool do Apache Spark sem servidor.

Pré-requisitos
Para concluir as etapas deste tutorial, você precisará ter acesso a um grupo de recursos no qual tenha a função Proprietário. Crie o workspace do Synapse nesse grupo de recursos.

Criar um workspace do Azure Synapse no portal do Azure
Iniciar o processo
Abra o portal do Azure e insira Synapse na barra de pesquisa sem pressionar Enter.
Nos resultados da pesquisa, em Serviços, selecione Azure Synapse Analytics.
Selecione Criar para criar um workspace.
Guia Informações Básicas > Detalhes do Projeto
Preencha os campos a seguir:

Assinatura – Escolha qualquer assinatura.
Grupo de recursos – Use qualquer grupo de recursos.
Grupo de recursos gerenciados – deixe em branco.
Guia Informações Básicas > Detalhes do Workspace
Preencha os campos a seguir:

Nome do workspace – Escolha qualquer nome exclusivo globalmente. Neste tutorial, usaremos myworkspace.
Região – escolha a região em que você colocou seus aplicativos/serviços cliente (por exemplo, VM do Azure, Power BI, Azure Analysis Services) e armazenamentos que contêm dados (por exemplo, armazenamento Azure Data Lake, armazenamento analítico do Azure Cosmos DB).

Em Selecionar o Data Lake Storage Gen 2:

Em Nome da conta, selecione Criar e dê à nova conta de armazenamento o nome contosolake ou outro nome semelhante, pois ele precisa ser exclusivo.
Em Nome do sistema de arquivos, selecione Criar e dê a ele o nome usuários. Isso criará um contêiner de armazenamento chamado usuários. O workspace usará essa conta de armazenamento como a conta de armazenamento "primária" para os logs do aplicativo e as tabelas do Spark.
Marque a caixa "Atribuir a função Colaborador de Dados do Blob de Armazenamento a mim mesmo na conta do Data Lake Storage Gen2".

## Conclusão do processo
Selecione Examinar + criar>Criar. Seu workspace fica pronto em alguns minutos.

# Atenção

> **Nem todos os recursos do pool de SQL dedicado nos workspaces do Azure Synapse se aplicam ao pool de SQL dedicado (antigo SQL DW) e vice-versa.**

[Clique aqui para ver as Diferenças](https://techcommunity.microsoft.com/t5/azure-synapse-analytics-blog/what-s-the-difference-between-azure-synapse-formerly-sql-dw-and/ba-p/3597772)

## Abrir o Synapse Studio
Após criar o workspace do Azure Synapse, você tem duas maneiras de abrir o Synapse Studio:

1. Abra o workspace do Azure Synapse no portal do Azure e, na seção Visão geral do workspace do Azure Synapse, selecione Abrir na caixa Abrir Synapse Studio.
2. Acesse https://web.azuresynapse.net e entre no seu workspace.

Fazer logon no espaço de trabalho

<img src="https://github.com/flavioafarias/synapse_trainning/blob/main/images/login-workspace.png" width="600" height="350"/>

## Colocar dados de exemplo na conta de armazenamento primária

Vamos usar um pequeno conjunto de dados de exemplo, com 100 mil linhas de dados de Táxis de NYC para muitos exemplos neste guia de introdução. Começamos colocando-o na conta de armazenamento primária que você criou para o espaço de trabalho.

* Baixe este arquivo no computador: <a href="https://github.com/flavioafarias/synapse_trainning/blob/main/files_support/NYCTripSmall.parquet" target="_blank" rel="noopener noreferrer">NYCTripSmall</a>.
* No Synapse Studio, navegue até o Hub de Dados.
* Selecione Vinculado.
* Na categoria Azure Data Lake Storage Gen2, você verá um item com um nome semelhante a myworkspace (Primário – contosolake) .
* Selecione o contêiner chamado usuários (Primário) .
* Selecione Carregar e selecione o arquivo NYCTripSmall.parquet que você baixou.

Depois de carregado, o arquivo parquet estará disponível por meio de dois URIs equivalentes:

* https://contosolake.dfs.core.windows.net/users/NYCTripSmall.parquet*
* abfss://users@contosolake.dfs.core.windows.net/NYCTripSmall.parquet*

Nos exemplos a seguir neste tutorial, certifique-se de substituir contosolake na interface do usuário pelo nome da conta de armazenamento primária que você selecionou para seu workspace.

# Analisar dados com um pool de SQL sem servidor

O pool de SQL sem servidor interno
Os pools de SQL sem servidor permitem que você use o SQL sem precisar reservar a capacidade. A cobrança de um pool de SQL sem servidor se baseia no volume de dados processados para executar a consulta, não no número de nós usados para executá-la.

Todo workspace é fornecido com um pool de SQL sem servidor pré-configurado chamado Interno.

Analisar dados de Táxi de NYC com um pool de SQL sem servidor

1. No Synapse Studio, acesse o hub Desenvolver
2. Crie um script SQL.
3. Cole o código a seguir no script.
    ```sql
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
            BULK 'https://contosolake.dfs.core.windows.net/users/NYCTripSmall.parquet',
            FORMAT='PARQUET'
        ) AS [result]```
4. Clique em Executar.

A exploração de dados é apenas um cenário simplificado no qual você pode entender as características básicas dos seus dados.

## Criar um banco de dados de exploração

Procure o conteúdo dos arquivos diretamente por meio do banco de dados master. Para alguns cenários de exploração de dados simples, não é preciso criar um banco de dados separado. No entanto, à medida que você continua a exploração de dados, o ideal é criar alguns objetos de utilitário, como:

* Fontes de dados externas que representam as referências nomeadas para contas de armazenamento.
* Credenciais no escopo do banco de dados que permitem especificar como se autenticar na fonte de dados externa.
* Usuários de banco de dados com as permissões para acessar algumas fontes de dados ou objetos de banco de dados.
* Exibições, procedimentos e funções de utilitário que você pode usar nas consultas.

1. Use o banco de dados master para criar um banco de dados separado para objetos de banco de dados personalizados. Não é possível criar objetos de banco de dados personalizados no banco de dados master.

    ```SQL
    CREATE DATABASE DataExplorationDB 
                    COLLATE Latin1_General_100_BIN2_UTF8

>Use uma ordenação com o sufixo _UTF8 para garantir que o texto UTF-8 seja convertido corretamente em colunas VARCHAR. Latin1_General_100_BIN2_UTF8 fornece o melhor desempenho nas consultas que leem dados de arquivos Parquet e contêineres do Cosmos DB.

2. Alternar de mestre para DataExplorationDB usando o comando a seguir. Você também pode usar o controle da interface do usuário para usar o banco de dados para alternar o banco de dados atual:

```SQL

Copiar
USE DataExplorationDB ```

3. No 'DataExplorationDB', crie objetos de utilitário, como credenciais e fontes de dados.

SQL

Copiar
CREATE EXTERNAL DATA SOURCE ContosoLake
WITH ( LOCATION = 'https://contosolake.dfs.core.windows.net'
