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
    USE DataExplorationDB

3. No 'DataExplorationDB', crie objetos de utilitário, como credenciais e fontes de dados.

    ```SQL
        CREATE EXTERNAL DATA SOURCE ContosoLake
        WITH (LOCATION = 'https://contosolake.dfs.core.windows.net')


> Uma fonte de dados externa pode ser criada sem uma credencial. Se uma credencial não existir, a identidade do chamador será usada para acessar a fonte de dados externa.

Opcionalmente, use o banco de dados 'DataExplorationDB' criado recentemente para criar um logon para um usuário no DataExplorationDB que acessará dados externos:


    ```sql
    CREATE LOGIN data_explorer WITH PASSWORD = 'My Very Strong Password 1234!'
    
    

4. Depois crie um usuário de banco de dados em 'DataExplorationDB' para o logon acima e conceda a permissão ADMINISTER DATABASE BULK OPERATIONS.

    ```sql
    Copiar
    CREATE USER data_explorer FOR LOGIN data_explorer;
    GO
    GRANT ADMINISTER DATABASE BULK OPERATIONS TO data_explorer;
    GO

5. Explore o conteúdo do arquivo usando o caminho relativo e a fonte de dados:

    ```SQL
    Copiar
    SELECT
        TOP 100 *
    FROM
        OPENROWSET(
                BULK '/users/NYCTripSmall.parquet',
                DATA_SOURCE = 'ContosoLake',
                FORMAT='PARQUET'
        ) AS [result]


6. Publicar suas alterações no workspace.

O banco de dados de exploração de dados é apenas um espaço reservado simples no qual você poderá armazenar os objetos de utilitário. O pool de SQL do Synapse permite que você faça muito mais e crie um data warehouse lógico, uma camada relacional criada com base nas fontes de dados do Azure.