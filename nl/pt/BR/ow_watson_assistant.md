---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

keywords: watson assistant, openwhisk, functions

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# {{site.data.keyword.conversationshort}} pacote 

O serviço do {{site.data.keyword.conversationfull}} combina o aprendizado de máquina, o
entendimento de língua natural e as ferramentas de diálogo integradas para criar fluxos de conversa entre
seus apps e seus usuários.
{: shortdesc}

O pacote do  {{site.data.keyword.conversationshort}}  contém as entidades a seguir. É possível
localizar detalhes adicionais na referência da API do {{site.data.keyword.conversationshort}}
clicando no nome da entidade.

| Entity | Digite | Parâmetros | Descrição |
| --- | --- | --- | --- |
| [`assistant-v1`](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html) | pacote | username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url,  | Trabalhe com o serviço  {{site.data.keyword.conversationshort}} . |
| [message](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#message) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,    input, alternate_intents, context, entities, intents, output,     nodes_visited_details,  | Obtenha a resposta para a entrada do usuário. |
| [create-workspace](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-workspace) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,   name, description, language, intents, entities, dialog_nodes, counterexamples, metadata, learning_opt_out,  | Criar uma área de trabalho. |
| [delete-workspace](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-workspace) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,  | Excluir uma área de trabalho. |
| [get-workspace](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-workspace) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     export,     include_audit,  | Obtenha informações sobre uma área de trabalho. |
| [list-workspaces](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-workspaces) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    page_limit,     include_count,     sort,     cursor,     include_audit,  | Listar áreas de trabalho. |
| [update-workspace](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-workspace) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,    name, description, language, intents, entities, dialog_nodes, counterexamples, metadata, learning_opt_out,     append,  | Atualizar uma área de trabalho. |
| [create-intent](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-intent) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,    intent, description, examples,  | Crie uma intenção. |
| [delete-intent](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-intent) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,  | Excluir uma intenção. |
| [get-intent](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-intent) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,     export,     include_audit,  | Obtenha informações sobre uma intenção. |
| [list-intents](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-intents) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, export, page_limit, include_count, sort, cursor, include_audit,  | Listar as intents. |
| [update-intent](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-intent) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,    new_intent, new_description, new_examples,  | Atualizar uma intenção. |
| [create-example](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-example) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, intent, text,  | Crie um exemplo de entrada do usuário. |
| [delete-example](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-example) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, intent, text,  | Exclua um exemplo de entrada do usuário. |
| [get-example](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-example) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,     text,     include_audit,  | Obter informações sobre um exemplo de entrada do usuário. |
| [list-examples](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-examples) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,     page_limit,     include_count,     sort,     cursor,     include_audit,  | Listar exemplos de entrada do usuário. |
| [update-example](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-example) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     intent,     text,    new_text,  | Atualize um exemplo de entrada do usuário. |
| [create-counterexample](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-counterexample) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, text,  | Crie um contra-exemplo. |
| [delete-counterexample](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-counterexample) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, text,  | Exclua um contra-exemplo. |
| [get-counterexample](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-counterexample) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     text,     include_audit,  | Obtenha informações sobre um contra-exemplo. |
| [list-counterexamples](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-counterexamples) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, page_limit, include_count, sort, cursor, include_audit,  | Listar contra-exemplos. |
| [update-counterexample](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-counterexample) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     text,    new_text,  | Atualize um contra-exemplo. |
| [create-entity](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-entity) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,    entity, description, metadata, values, fuzzy_match,  | Criar uma entidade. |
| [delete-entity](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-entity) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,  | Excluir uma entidade. |
| [get-entity](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-entity) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     export,     include_audit,  | Obtenha informações sobre uma entidade. |
| [list-entities](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-entities) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, export, page_limit, include_count, sort, cursor, include_audit,  | Listar entidades. |
| [update-entity](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-entity) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,    new_entity, new_description, new_metadata, new_fuzzy_match, new_values,  | Atualizar uma entidade. |
| [create-value](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-value) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,    value, metadata, synonyms, patterns, value_type,  | Incluir um valor de entidade. |
| [delete-value](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-value) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,  | Exclua um valor de entidade. |
| [get-value](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-value) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,     export,     include_audit,  | Obtenha um valor de entidade. |
| [list-values](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-values) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     export,     page_limit,     include_count,     sort,     cursor,     include_audit,  | Listar valores de entidade. |
| [update-value](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-value) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,    new_value, new_metadata, new_type, new_synonyms, new_patterns,  | Atualize um valor de entidade. |
| [create-synonym](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-synonym) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, entity, value, synonym,  | Incluir um sinônimo de valor de entidade. |
| [delete-synonym](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-synonym) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, entity, value, synonym,  | Exclua um sinônimo de valor de entidade. |
| [get-synonym](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-synonym) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,     synonym,     include_audit,  | Obter um sinônimo de valor de entidade. |
| [list-synonyms](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-synonyms) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,     page_limit,     include_count,     sort,     cursor,     include_audit,  | Listar sinônimos de valor de entidade. |
| [update-synonym](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-synonym) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     entity,     value,     synonym,    new_synonym,  | Atualizar um sinônimo de valor da entidade. |
| [create-dialog-node](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#create-dialog-node) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,    dialog_node, description, conditions, parent, previous_sibling, output, context, metadata, next_step, actions, title, node_type, event_name, variable, digress_in, digress_out, digress_out_slots,  | Crie um nó de diálogo. |
| [delete-dialog-node](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-dialog-node) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     dialog_node,  | Excluir um nó de diálogo. |
| [get-dialog-node](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#get-dialog-node) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     dialog_node,     include_audit,  | Obtenha um nó de diálogo. |
| [list-dialog-nodes](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-dialog-nodes) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, workspace_id, page_limit, include_count, sort, cursor, include_audit,  | Listar nós de diálogo. |
| [update-dialog-node](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#update-dialog-node) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     dialog_node,    new_dialog_node, new_description, new_conditions, new_parent, new_previous_sibling, new_output, new_context, new_metadata, new_next_step, new_title, new_type, new_event_name, new_variable, new_actions, new_digress_in, new_digress_out, new_digress_out_slots,  | Atualizar um nó de diálogo. |
| [list-all-logs](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-all-logs) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    filter,     sort,     page_limit,     cursor,  | Listar eventos de log em todas as áreas de trabalho. |
| [list-logs](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#list-logs) | ação |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    workspace_id,     sort,     filter,     page_limit,     cursor,  | Listar eventos de log em uma área de trabalho. |
| [delete-user-data](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html?curl#delete-user-data) | ação |  username, password, iam_access_token, iam_apikey, iam_url, headers, headers[X-Watson-Learning-Opt-Out], url, customer_id,  | Exclua os dados rotulados. |

## Criando uma instância de serviço do  {{site.data.keyword.conversationshort}}
{: #service_instance_conversation}

Antes de instalar o pacote, deve-se criar uma instância de serviço e credenciais de serviço do
{{site.data.keyword.conversationshort}}.

1. [Crie uma instância de serviço do {{site.data.keyword.conversationshort}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/catalog/services/conversation).
2. Quando a instância de serviço for criada, as credenciais de serviço geradas automaticamente também serão criadas para você.

## Instalando o pacote do  {{site.data.keyword.conversationshort}}
{: #install_conversation}

Depois que você tem uma instância de serviço do {{site.data.keyword.conversationshort}}, use a CLI
do {{site.data.keyword.openwhisk}} para instalar o pacote do
{{site.data.keyword.conversationshort}} em seu namespace.
{: shortdesc}

### Instalando a partir da CLI do  {{site.data.keyword.openwhisk_short}}
{: #conversation_cli}

Antes de Iniciar:
  1. [ Instale o plug-in do  {{site.data.keyword.openwhisk_short}}  para a  {{site.data.keyword.Bluemix_notm}}  CLI ](/docs/openwhisk?topic=cloud-functions-cloudfunctions_cli#cloudfunctions_cli).

Para instalar o pacote do  {{site.data.keyword.conversationshort}} :

1. Clone o repo do pacote do  {{site.data.keyword.conversationshort}} .
    ```
    git clone https://github.com/watson-developer-cloud/openwhisk-sdk
    ```
    {: pre}

2. Implemente o pacote.
    ```
    ibmcloud fn deploy -m openwhisk-sdk/packages/assistant-v1/manifest.yaml
    ```
    {: pre}

3. Verifique se o pacote foi incluído em sua lista de pacotes.
    ```
    ibmcloud fn package list
    ```
    {: pre}

    Saída:
    ```
    packages
    /myOrg_mySpace/assistant-v1                        private
    ```
    {: screen}

4. Ligue as credenciais da instância do {{site.data.keyword.conversationshort}} que você criou
ao pacote.
    ```
    ibmcloud fn service bind bind Assistant-v1
    ```
    {: pre}

    Exemplo de Saída:
    ```
    Credentials 'Credentials-1' from 'conversation' service instance 'Watson Assistant (formerly Conversation)-8h' bound to 'assistant-v1'.
    ```
    {: screen}

5. Verifique se o pacote está configurado com suas credenciais de instância de serviço do
{{site.data.keyword.conversationshort}}.
    ```
    ibmcloud fn package get Assistant-v1 parameters
    ```
    {: pre}

    Exemplo de Saída:
    ```
    ok: got package assistant-v1, displaying field parameters
    [
      {
        "key": "__bx_creds",
            "value": {
          "conversation": {
            "credentials": "Credentials-1",
            "instance": "Watson Assistant (formerly Conversation)-8h",
            "password": "AAAA0AAAAAAA",
            "url": "https://gateway.watsonplatform.net/assistant/api",
            "username": "00a0aa00-0a0a-12aa-1234-a1a2a3a456a7"
          }
        }
      }
    ]
    ```
    {: screen}

### Instalando a partir da UI do  {{site.data.keyword.openwhisk_short}}
{: #conversation_ui}

1. No console do {{site.data.keyword.openwhisk_short}}, acesse a [página Criar ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/openwhisk/create).

2. Usando as listas **Organização do Cloud Foundry** e **Espaço do Cloud Foundry**, selecione o namespace no qual você deseja instalar o pacote. Os namespaces são formados por meio de nomes de organização e de espaço combinados.

3. Clique em  ** Instalar pacotes **.

4. Clique no grupo de pacotes do  ** Watson ** .

5. Clique no Pacote **Watson Assistant**.

5. Clique em  ** Instalar **.

6. Depois que o Pacote tiver sido instalado, você será redirecionado para a página Ações e poderá
procurar pelo seu novo Pacote, que é denominado **assistant-v1**.

7. Para usar as Ações no pacote **assistant-v1**, deve-se ligar as credenciais
de serviço às ações.
  * Para ligar as credenciais de serviço a todas as ações no pacote, siga as etapas 5 e 6 nas instruções da CLI listadas acima.
  * Para ligar as credenciais de serviço a ações individuais, conclua as etapas a seguir na IU. **Nota**: deve-se concluir as etapas a seguir para cada ação que você deseja usar.
    1. Clique em uma ação por meio do Pacote **assistant-v1** que você deseja usar. A página de detalhes para essa ação é aberta.
    2. Na navegação à esquerda, clique na seção **Parâmetros**.
    3. Insira um novo  ** parâmetro **. Para a chave, insira  ` __bx_creds `. Para o valor, cole no objeto da JSON de credenciais de serviço por meio da instância de serviço que você criou anteriormente.

## Usando o pacote do  {{site.data.keyword.conversationshort}}
{: #usage_conversation}

Para usar as ações neste pacote, execute comandos no formato a seguir:

```
ibmcloud fn action invoke assistant-v1/<action_name> -b -p <param name> <param>
```
{: pre}

Todas as ações exigirão um parâmetro de versão no formato AAAA-MM-DD. Quando a API mudar de uma maneira inversa de forma incompatível, uma nova data da versão será liberada. Consulte mais detalhes na
[Referência da API](https://www.ibm.com/watson/developercloud/assistant/api/v1/curl.html#versioning).

As funções deste pacote usam a versão atual do Watson Assistant, 2018-07-10. Experimente a ação  ` list-workspaces ` .
```
ibmcloud fn action invoke assistant-v1/list-workspaces -b -p version 2018-07-10
```
{: pre}
