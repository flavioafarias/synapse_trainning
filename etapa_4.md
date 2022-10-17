# Análise com o Apache Spark

## Criar um Pool do Apache Spark sem servidor

1. No Synapse Studio, no painel do lado esquerdo, selecione Gerenciar>Pools do Apache Spark.
2. Selecione Novo
3. Em Nome do Pool do Apache Spark, insira Spark1.
4. Em Tamanho do nó, insira Pequeno.
5. Em Número de nós, defina o mínimo como 3 e o máximo como 3
6. Selecione Examinar + criar>Criar. Seu Pool do Apache Spark estará pronto em alguns segundos.

## Noções básicas sobre pools do Apache Spark sem servidor

Um Pool do Spark sem servidor é uma forma de indicar como um usuário deseja trabalhar com o Spark. Quando você começa a usar um pool, uma sessão do Spark é criada, se necessário. O pool controla quantos recursos do Spark serão usados por essa sessão e quanto tempo a sessão vai durar antes de ser colocada em pausa automaticamente. Você paga pelos recursos do Spark usados durante essa sessão, não pelo próprio pool. Dessa forma, um Pool do Spark permite que você trabalhe com o Spark, sem precisar se preocupar com o gerenciamento de clusters. Isso é semelhante a como funciona um pool de SQL sem servidor.

## Analisar dados de Táxi de NYC com um pool do Spark

1. No Synapse Studio, acesse o hub Desenvolver.
2. Crie um novo bloco de anotações.
3. Crie uma célula de código e cole o seguinte código nela:

    ```python
            %%pyspark
            df = spark.read.load('abfss://users@contosolake.dfs.core.windows.net/NYCTripSmall.parquet', format='parquet')
            display(df.limit(10))

4. Modifique o URI de carregamento para que ele referencie o arquivo de exemplo na sua conta de armazenamento de acordo com o esquema de URI abfss.

5. No notebook, no menu Anexar a, escolha o Pool do Spark sem servidor Spark1 que criamos anteriormente.

6. Selecione Executar na célula. O Azure Synapse iniciará uma nova sessão do Spark para executar essa célula, se necessário. Se uma nova sessão do Spark for necessária, inicialmente, levará cerca de dois segundos para que ela seja criada.

7. Se você quiser ver apenas o esquema do dataframe, execute uma célula com o seguinte código:

    ```python
            %%pyspark
            df.printSchema()

## Carregar os dados de táxi de Nova York no banco de dados nyctaxi do Spark

Os dados ficam disponíveis por meio do dataframe chamado df. Carregue-os em um banco de dados do Spark chamado nyctaxi.

1. Adicione uma nova célula de código ao notebook e insira o seguinte código:

    ```python
        %%pyspark
        spark.sql("CREATE DATABASE IF NOT EXISTS nyctaxi")
        df.write.mode("overwrite").saveAsTable("nyctaxi.trip")

## Analisar os dados de táxi de NYC usando Spark e notebooks

1. Crie uma célula de código e insira o código a seguir.
    
    ```python
        %%pyspark
        df = spark.sql("SELECT * FROM nyctaxi.trip")
        display(df)

2. Execute a célula para mostrar os dados de Táxis de Nova York que carregamos no banco de dados nyctaxi do Spark.
3. Crie uma célula de código e insira o código a seguir. Analisaremos esses dados e salvaremos os resultados em uma tabela chamada nyctaxi.passengercountstats.

    ```python
        %%pyspark
        df = spark.sql("""SELECT PassengerCount,
        SUM(TripDistanceMiles) as SumTripDistance,
        AVG(TripDistanceMiles) as AvgTripDistance
        FROM nyctaxi.trip
        WHERE TripDistanceMiles > 0 AND PassengerCount > 0
        GROUP BY PassengerCount
        ORDER BY PassengerCount""") 
        display(df)
        df.write.saveAsTable("nyctaxi.passengercountstats")

4. Nos resultados da célula, selecione Gráfico para visualizar os dados exibidos.