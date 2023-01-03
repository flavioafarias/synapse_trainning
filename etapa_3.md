# Analisar com Data Explorer (versão prévia)

### Criar um pool do Data Explorer

No Synapse Studio, no painel do lado esquerdo, selecione Gerenciar>Pools do Data Explorer.

Selecione Novo e insira os seguintes detalhes na guia Noções básicas:


| Configuração        | Valor sugerido           | Descrição  |
|:-------------: |:-------------:| :-----: |
| Nome do pool do Data Explorer | contosodataexplorer | Este é o futuro nome do pool do Data Explorer. |
| Carga de trabalho|Otimizado para computação|Esta carga de trabalho fornece uma CPU maior para a taxa de armazenamento SSD. |
| Tamanho do nó | Pequeno (4 núcleos)|Defina isso com o menor tamanho para reduzir os custos deste início rápido |



>Observe que há limitações específicas para os nomes que os pools do Data Explorer podem usar. Os nomes devem conter apenas letras minúsculas e números, ter entre 4 e 15 caracteres e começar com uma letra.

3. Selecione Examinar + criar>Criar. O pool do Data Explorer iniciará o processo de provisionamento.

## Criar um banco de dados do Data Explorer

1. No Synapse Studio, no painel esquerdo, selecione Dados.

2. Selecione + (Adicionar novo recurso) >Banco de dados do Data Explorer e cole as seguintes informações:

    | Configuração	| Valor sugerido	| Descrição |
    |-------------|:---------------:|-------------|
    | Nome do pool	| contosodataexplorer	| O nome do pool do Data Explorer a ser usado |
    | Nome	| TestDatabase	| O nome do banco de dados deve ser exclusivo dentro do cluster. |
    | Período de retenção padrão	| 365	| O período de tempo (em dias) durante o qual há a garantia de que os dados serão mantidos disponíveis para consulta.	| O período é medido a partir do momento em que os dados são incluídos. |
    | Período de cache padrão	| 31	| O período de tempo (em dias) durante o qual os dados consultados com frequência devem ser mantidos disponíveis no armazenamento SSD ou RAM, em vez de no armazenamento de longo prazo. |

3. Selecione Criar para criar o banco de dados. A criação geralmente leva menos de um minuto.

## Ingerir dados de exemplo e analisar com uma consulta simples

1. No Synapse Studio, no painel do lado esquerdo, selecione Desenvolver.
2. Em Scripts KQL, selecione + (Adicionar novo recurso) >Script KQL. No painel do lado direito, você pode nomear o script.
3. No menu Conexão, selecione contosodataexplorer.
4. No menu Usar banco de dados, selecione TestDatabase.
5. Cole o comando a seguir e selecione Executar para criar uma tabela StormEvents.

        ''sql
        .create table StormEvents (StartTime: datetime, EndTime: datetime, EpisodeId: int, EventId: int, State: string, EventType: string, InjuriesDirect: int, InjuriesIndirect: int, DeathsDirect: int, DeathsIndirect: int, DamageProperty: int, DamageCrops: int, Source: string, BeginLocation: string, EndLocation: string, BeginLat: real, BeginLon: real, EndLat: real, EndLon: real, EpisodeNarrative: string, EventNarrative: string, StormSummary: dynamic)


    > Dica

    > Verifique se a tabela foi criada com êxito. No painel esquerdo, selecione Dados, selecione o menu contosodataexplorer e, em seguida, selecione Atualizar. Em contosodataexplorer, expanda Tabelas e verifique se a tabela StormEvents é exibida na lista.

6. Cole o comando a seguir e selecione Executar para ingerir dados na tabela StormEvents.

    ```sql
    .ingest into table StormEvents 'https://kustosamplefiles.blob.core.windows.net/samplefiles/StormEvents.csv?sv=2019-12-12&ss=b&srt=o&sp=r&se=2022-09-05T02:23:52Z&st=2020-09-04T18:23:52Z&spr=https&sig=VrOfQMT1gUrHltJ8uhjYcCequEcfhjyyMX%2FSc3xsCy4%3D' with (ignoreFirstRecord=true)

7. Depois que o processamento for concluído, cole a consulta a seguir, selecione a consulta na janela e selecione Executar.

    ```sql
        StormEvents
        | sort by StartTime desc
        | take 10

8. A consulta retorna os seguintes resultados dos dados de amostra ingeridos.

sample-query-results.png
