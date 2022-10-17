Visualizar os dados com o Power BI
Artigo
27/09/2022
3 minutos para o fim da leitura
6 colaboradores


Neste tutorial, você aprenderá a criar um workspace do Power BI, vincular seu workspace do Azure Synapse e criar um conjunto de dados do Power BI que utiliza os dados no workspace do Azure Synapse.

Pré-requisitos
Para concluir este tutorial, instale o Power BI Desktop.

Visão geral
Com base nos dados de táxi de Nova York, criamos conjuntos de dados agregados em duas tabelas:

nyctaxi.passengercountstats
SQLDB1.dbo.PassengerCountStats
Você pode vincular um workspace do Power BI ao seu workspace do Azure Synapse. Essa funcionalidade permite que você obtenha dados com facilidade em seu workspace do Power BI. Você pode editar os relatórios de Power BI diretamente no seu workspace do Azure Synapse.

Criar um workspace do Power BI
Entre no powerbi.microsoft.com.
Clique em Workspaces e selecione Criar um workspace. Crie um workspace do Power BI chamado NYCTaxiWorkspace1 ou outro nome semelhante, pois esse nome precisa ser exclusivo.
Vincular seu workspace do Azure Synapse ao novo workspace do Power BI
No Synapse Studio, vá para Gerenciar>Serviços Vinculados.
Selecione Novo>Conectar-se ao Power BI.
Defina Nome como NYCTaxiWorkspace1.
Defina Nome do workspace como o workspace do Power BI criado acima, semelhante a NYCTaxiWorkspace1.
Selecione Criar.
Criar um conjunto de dados do Power BI que use dados em seu workspace do Azure Synapse
No Synapse Studio, acesse Desenvolver>Power BI.
Navegue até NYCTaxiWorkspace1>Conjuntos de dados do Power BI e selecione Novo conjunto de dados do Power BI. Clique em Iniciar.
Selecione a fonte de dados SQLPOOL1 e clique em Continuar.
Clique em Baixar para baixar o arquivo .pbids para o arquivo NYCTaxiWorkspace1SQLPOOL1.pbids. Clique em Continue.
Abra o arquivo .pbids baixado. O Power BI Desktop será aberto e se conectará automaticamente ao SQLDB1 no workspace do Azure Synapse.
Se uma caixa de diálogo chamada Banco de dados do SQL Server for exibida:
Selecione Conta Microsoft.
Selecione Entrar e entre na conta.
Selecione Conectar.
Depois que a caixa de diálogo Navegador for aberta, verifique a tabela PassengerCountStats e selecione Carregar.
Depois que a caixa de diálogo Configurações de conexão for exibida, selecione DirectQuery>OK.
Selecione o botão Relatório à esquerda.
Em Visualizações, clique no ícone do gráfico de linhas para adicionar um Gráfico de linhas ao relatório.
Em Campos, arraste a coluna PassengerCount para Visualizações>Eixo.
Arraste as colunas SumTripDistance e AvgTripDistance para Visualizações>Valores.
Na guia Página Inicial, selecione Publicar.
Selecione Salvar para salvar as alterações.
Escolha o nome do arquivo PassengerAnalysis.pbix e, em seguida, selecione Salvar.
Na janela Publicar no Power BI, em Selecionar um destino, escolha o NYCTaxiWorkspace1 e clique em Selecionar.
Aguarde a conclusão da publicação.
Configurar autenticação para o conjunto de dados
Abra powerbi.microsoft.com e escolha Entrar.
No lado esquerdo, em Workspaces, selecione o workspace NYCTaxiWorkspace1.
Dentro desse workspace, localize um conjunto de dados chamado de Análise de Passageiros e um relatório chamado Análise de Passageiros.
Passe o mouse sobre o conjunto de dados PassengerAnalysis, selecione o botão de reticências (...) e, em seguida, selecione Configurações.
Em Credenciais da fonte de dados, clique em Editar, defina o Método de autenticação como OAuth2 e selecione Entrar.
Editar um relatório no Synapse Studio
Volte para o Synapse Studio e selecione Fechar e atualizar.
Acesse o hub Desenvolver.
À direita da camada do Power BI, clique no botão de reticências (...) e clique em Atualizar para atualizar o nó Relatórios do Power BI.
Agora, em Power BI, você deve ver:
Em NYCTaxiWorkspace1>Conjunto de dados do Power BI, um novo conjunto de dados chamado PassengerAnalysis.
Em NYCTaxiWorkspace1>Relatórios do Power BI, um novo relatório chamado PassengerAnalysis.
Selecione o relatório PassengerAnalysis. O relatório é aberto e você pode editá-lo diretamente no Synapse Studio.