# Analisar dados com pools de SQL dedicados

## Criar um pool de SQL dedicado

1. No Synapse Studio, no painel do lado esquerdo, selecione Gerenciar>Pools de SQL em pools de Análise.
2. Selecione Novo
3. Em Nome do pool de SQL dedicado, selecione SQLPOOL1
4. Em Nível de desempenho, escolha DW100C
5. Selecione Examinar + criar>Criar. Seu pool de SQL dedicado estará pronto em alguns minutos.

O pool de SQL dedicado é associado a um Banco de Dados SQL também chamado SQLPOOL1.

1. Acesse Dados>Workspace.
2. Você deverá ver um banco de dados chamado SQLPOOL1. Se você não vir o comando, clique em Atualizar.

Um pool de SQL dedicado consome recursos faturáveis desde que ele esteja ativo. Você pode pausar o pool posteriormente para reduzir custos.

##Carregar os dados de Táxi de Nova York no SQLPOOL1

1. No Synapse Studio, navegue até o hub Desenvolver, clique no botão + para adicionar um novo recurso e crie um script SQL.

2. Selecione o pool 'SQLPOOL1' (pool criado na ETAPA 1 deste tutorial) na lista suspensa Conectar-se a, acima do script.

3. Insira o seguinte código:

        ```sql
            IF NOT EXISTS (SELECT * FROM sys.objects O JOIN sys.schemas S ON O.schema_id = S.schema_id WHERE O.NAME = 'NYCTaxiTripSmall' AND O.TYPE = 'U' AND S.NAME = 'dbo')
            
            CREATE TABLE dbo.NYCTaxiTripSmall
            (
                [DateID] int,
                [MedallionID] int,
                [HackneyLicenseID] int,
                [PickupTimeID] int,
                [DropoffTimeID] int,
                [PickupGeographyID] int,
                [DropoffGeographyID] int,
                [PickupLatitude] float,
                [PickupLongitude] float,
                [PickupLatLong] nvarchar(4000),
                [DropoffLatitude] float,
                [DropoffLongitude] float,
                [DropoffLatLong] nvarchar(4000),
                [PassengerCount] int,
                [TripDurationSeconds] int,
                [TripDistanceMiles] float,
                [PaymentType] nvarchar(4000),
                [FareAmount] numeric(19,4),
                [SurchargeAmount] numeric(19,4),
                [TaxAmount] numeric(19,4),
                [TipAmount] numeric(19,4),
                [TollsAmount] numeric(19,4),
                [TotalAmount] numeric(19,4)
            )
            WITH
                (
                DISTRIBUTION = ROUND_ROBIN,
                CLUSTERED COLUMNSTORE INDEX
                -- HEAP
                )
            GO

            COPY INTO dbo.NYCTaxiTripSmall
            (DateID 1, MedallionID 2, HackneyLicenseID 3, PickupTimeID 4, DropoffTimeID 5,
            PickupGeographyID 6, DropoffGeographyID 7, PickupLatitude 8, PickupLongitude 9, 
            PickupLatLong 10, DropoffLatitude 11, DropoffLongitude 12, DropoffLatLong 13, 
            PassengerCount 14, TripDurationSeconds 15, TripDistanceMiles 16, PaymentType 17, 
            FareAmount 18, SurchargeAmount 19, TaxAmount 20, TipAmount 21, TollsAmount 22, 
            TotalAmount 23)
            FROM 'https://contosolake.dfs.core.windows.net/users/NYCTripSmall.parquet'
            WITH
            (
                FILE_TYPE = 'PARQUET'
                ,MAXERRORS = 0
                ,IDENTITY_INSERT = 'OFF'
            )

4. Clique no botão Executar para executar o script.

5. Esse script será concluído em menos de 60 segundos. Ele carrega 2 milhões de linhas de dados dos táxis de Nova York em uma tabela chamada dbo.NYCTaxiTripSmall.

## Explorar os dados de táxis de Nova York no pool de SQL dedicado

1. No Synapse Studio, acesse o hub Dados.
2. Acesse SQLPOOL1>Tabelas.
3. Clique com o botão direito do mouse na tabela dbo.NYCTaxiTripSmall e selecione Novo Script de SQL>Selecionar as Primeiras 100 Linhas.
4. Aguarde enquanto um novo script SQL é criado e executado.
5. Observe na parte superior do script de SQL que Conectar-se ao é automaticamente definido como o pool de SQL chamado SQLPOOL1.
6. Substitua o texto do script de SQL por esse código e execute-o.

    ```sql
        SELECT  PassengerCount,
                SUM(TripDistanceMiles) as SumTripDistance,
                AVG(TripDistanceMiles) as AvgTripDistance
        FROM  dbo.NYCTaxiTripSmall
        WHERE TripDistanceMiles > 0 AND PassengerCount > 0
        GROUP BY PassengerCount
        ORDER BY PassengerCount;

Essa consulta mostra como as distâncias totais de viagem e a distância média da viagem estão relacionadas ao número de passageiros.

7. Na janela de resultados do script de SQL, altere a opção Exibição para Gráfico para uma visualização dos resultados como um gráfico de linhas.