# Synapse Analytics Trainning
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

> **Nem todos os recursos do pool de SQL dedicado nos workspaces do Azure Synapse se aplicam ao pool de SQL dedicado (antigo SQL DW) e vice-versa. Este artigo é um guia** > para habilitar os recursos do workspace para um pool de SQL dedicado existente (antigo SQL DW).
