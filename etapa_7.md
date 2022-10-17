#Fazer a integração a pipelines

##Criar um pipeline e adicionar uma atividade de notebook

1. No Synapse Studio, acesse o hub Integrar.
2. Selecione+>Pipeline para criar um novo pipeline. Clique no novo objeto de pipeline para abrir o Designer de Pipeline.
3. Em Atividades, expanda a pasta Synapse e arraste um objeto Notebook para o designer.
4. Selecione a guia Configurações das propriedades da atividade do Notebook. Use a lista suspensa para escolher um notebook do workspace atual do Azure Synapse.

##Agendar o pipeline para ser executado de hora em hora

1. No pipeline, selecione Adicionar gatilho>Novo/editar.
2. Em Escolher gatilho, selecione Novo e defina Recorrência como "a cada 1 hora".
3. Selecione OK.
4. Selecione Publicar Tudo.

##Forçando a execução imediata de um pipeline

Depois que o pipeline for publicado, talvez você queira executá-lo imediatamente sem esperar passar uma hora.

1. Abra o pipeline.
2. Clique em Adicionar gatilho>Disparar agora.
3. Selecione OK.

##Monitorar a execução do pipeline

1. Vá para o hub Monitorar.
2. Selecione Execuções de pipeline para monitorar o andamento da execução do pipeline.
3. Nessa exibição, você pode alternar entre a exibição de uma lista tabular e um gráfico de Gantt.
4. Clique em um nome de pipeline para ver o status das atividades nesse pipeline.