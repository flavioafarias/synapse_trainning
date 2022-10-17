#Explorar o Centro de Conhecimento do Azure Synapse

## Como localizar o Centro de conhecimento

Há duas maneiras de localizar o Centro de conhecimento no Synapse Studio:

1. No hub inicial, ao lado da parte superior da página, clique em Learn.
2. Na barra de menus na parte superior, clique em ? e em Centro de conhecimento.
Escolha um dos métodos e abra o Centro de conhecimento.

##Explorando o centro de Conhecimento

Quando estiver visível, você verá que o Centro de conhecimento permite fazer três coisas:

* Use amostras imediatamente. Se você quiser um exemplo rápido de como o Azure Synapse funciona, escolha essa opção.
* Procurar na galeria. Essa opção permite vincular conjuntos de dados de exemplo e adicionar código de exemplo na forma de scripts SQL, notebooks e pipelines.
* Conheça o Synapse Studio. Essa opção o levará em um breve tour pelas partes básicas do Synapse Studio. Isso será útil se você nunca tiver usado o Synapse Studio.

##Use os exemplos imediatamente: três exemplos para ajudá-lo a começar rapidamente

Há três itens nesta seção:

* Explorar dados de exemplo com o Spark
* Consultar dados com SQL
* Criar tabela externa com SQL

1. No Centro de conhecimento, clique em Usar amostras imediatamente.
2. Selecione Consultar dados com SQL.
3. Clique em Usar exemplo.
4. Um novo script SQL de exemplo será aberto.
5. Role o conteúdo até a primeira consulta (linhas 28 a 32) e selecione o texto da consulta.
6. Clique em Executar. Ele executará apenas o código selecionado.

##Galeria: uma coleção de conjuntos de dados e de códigos de exemplo

1. Acesse o Centro de conhecimento e clique em Procurar na galeria.
2. Selecione a guia Scripts SQL na parte superior.
3. Escolha o exemplo de ingestão de dados Carregar o conjunto de dados de Táxis de Nova York e clique em Continuar.
4. Em Pool de SQL, escolha Selecionar um pool existente, escolha SQLPOOL1 e o banco de dados SQLPOOL1 criado anteriormente.
5. Clique em Abrir Script.
6. Um novo script SQL de exemplo será aberto.
7. Clique em Executar
8. Isso criará várias tabelas para todos os dados de táxi de NYC e as carregará usando o comando COPY do T-SQL. Se você tiver criado essas tabelas nas etapas anteriores do guia de início rápido, selecione e execute apenas o código para CRIAR e COPIAR para tabelas que não existem.

>Observação
Ao usar a galeria de exemplos para o script SQL com um pool de SQL dedicado (antigo SQL DW), você só poderá usar um pool de SQL dedicado (antigo SQL DW).