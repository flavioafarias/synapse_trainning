#Monitorar o workspace do Synapse

##Introdução ao Hub de monitoramento

Abra o Synapse Studio e navegue até o hub de Monitoramento. Aqui você poderá ver um histórico de todas as atividades que estão ocorrendo no workspace e quais estão ativas no momento.

* Em Integração, você pode monitorar pipelines, gatilhos e runtimes de integração.
* Em Atividades, você pode monitorar atividades do Spark e do SQL.

##Integração

1. Navegue até Integração > Execuções de pipeline. Nessa exibição, você pode ver toda vez que um pipeline é executado em seu workspace.
2. Localize o pipeline que você executou na etapa anterior e clique no respectivo Nome de pipeline para exibir os detalhes.
3. Clique em Barra de trilha perto da parte superior do Synapse Studio, clique em Todas as execuções de pipeline para retornar à exibição anterior.

##Atividades do Data Explorer

1. Navegue até Atividades > Solicitações KQL.
2. Nesta exibição, você pode ver solicitações KQL.
3. Selecione um Pool a ser monitorado no filtro Pool. Agora você pode ver todas as solicitações KQL que estão em execução ou foram executadas em seu workspace nesse pool.
4. Localize uma solicitação KQL específica e clique no link Mais para ver o texto completo da solicitação KQL.

##Atividades do Apache Spark

1. Navegue até Atividades > Aplicativos Apache Spark. Agora você pode ver todos os aplicativos Spark em execução ou que foram executados em seu workspace.
2. Localize um aplicativo que não esteja mais em execução e clique em Nome de aplicativo. Agora você pode ver os detalhes do aplicativo Spark.
3. Se você estiver familiarizado com Apache Spark, poderá encontrar a interface do usuário do servidor de histórico do Apache Spark padrão clicando em Servidor de histórico do Spark.

##Atividades do SQL

1. Navegue até Atividades > Solicitações SQL.
2. Nesta exibição, você pode ver solicitações SQL.
3. Selecione um Pool a ser monitorado no filtro Pool. Agora você pode ver todas as solicitações SQL que estão em execução ou foram executadas em seu workspace nesse pool.
4. Localize uma solicitação SQL específica e clique no link Mais para ver o texto completo da solicitação SQL.

>Observação
As solicitações SQL enviadas por meio do Synapse Studio em um pool de SQL dedicado habilitado para workspace (antigo SQL DW) podem ser exibidas no hub do monitor. Para todas as outras atividades de monitoramento, você pode acessar o monitoramento do pool de SQL dedicado do portal do Azure (antigo SQL DW).