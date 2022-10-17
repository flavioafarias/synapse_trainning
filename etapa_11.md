#Adicionar um administrador ao workspace do Azure Synapse

##Visão geral

Até agora, no guia de introdução, nós nos concentramos nas atividades que você mesmo faz no workspace. Como você criou o workspace na ETAPA 1, você é o administrador do workspace do Azure Synapse. Agora, transformaremos outro usuário, Ryan (ryan@contoso.com), em um administrador. Quando terminarmos, Ryan será capaz de fazer tudo o que você pode fazer no workspace.

##RBAC do Azure: função de proprietário do workspace

1. Abra o portal do Azure e o workspace do Azure Synapse.
2. No lado esquerdo, selecione Controle de acesso (IAM) .
3. Selecione Adicionar>Adicionar atribuição de função para abrir a página Adicionar atribuição de função.
4. Atribua a função a seguir. Para ver as etapas detalhadas, confira Atribuir funções do Azure usando o portal do Azure.

|Configuração |	Valor |
|-------------|:-----:|
| Função | Proprietário |
| Atribuir acesso a | USER |
| Membro | ryan@contoso.com |

Add role assignment page in Azure portal. (Imagem)

5. Clique em Salvar.

## RBAC do Synapse: função de administrador do Azure Synapse para o workspace

Atribua a ryan@contoso.com a função RBAC de Administrador do Azure Synapse no workspace.

1. Abra o workspace no Azure Synapse Studio.
2. No lado esquerdo, selecione Gerenciar para abrir o hub Gerenciar.
3. Em Segurança, selecione Controle de acesso.
4. Selecione Adicionar.
5. Mantenha o Escopo configurado como Workspace.
6. Adicione ryan@contoso.com para a função Administrador do Azure Synapse.
7. Em seguida, selecione Aplicar.

## RBAC do Azure: atribuições de funções na conta de armazenamento primária do workspace

1. Abra a conta de armazenamento principal do workspace no portal do Azure.
2. No lado esquerdo, selecione Controle de acesso (IAM) .
3. Selecione Adicionar>Adicionar atribuição de função para abrir a página Adicionar atribuição de função.
4. Atribua a função a seguir. Para ver as etapas detalhadas, confira Atribuir funções do Azure usando o portal do Azure.

| Configuração | Valor |
|--------------|:-----:|
| Função 1 | Proprietário |
| Função 2 | Colaborador de Dados do Azure Storage Blob |
| Atribuir acesso a | USER |
| Membro | ryan@contoso.com |

Add role assignment page in Azure portal. (Imagem)

## Pools de SQL dedicados: função db_owner

Atribua ryan@contoso.com ao db_owner em cada pool de SQL dedicado no workspace.

        ```sql
            CREATE USER [ryan@contoso.com] FROM EXTERNAL PROVIDER; 
            EXEC sp_addrolemember 'db_owner', 'ryan@contoso.com'