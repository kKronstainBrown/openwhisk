---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

keywords: namespaces, actions, create

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}

# Création d'espaces de nom
{: #openwhisk_namespaces}

Dans la région Tokyo, {{site.data.keyword.openwhisk_short}} utilise des espaces de nom gérés par Identity and Access (IAM) pour regrouper des entités, telles que des actions ou des déclencheurs. Vous pouvez ensuite créer des règles d'accès pour l'espace de nom.
{: shortdesc}

Lorsque vous créez un espace de nom {{site.data.keyword.openwhisk_short}}, il est identifié en tant qu'instance de service IAM. Les instances de service gérées par IAM doivent être créées dans un [groupe de ressources](/docs/resources?topic=resources-rgs). Vous pouvez soit créer votre propre groupe de ressources, soit cibler le groupe de ressources par défaut. Pour voir les instances de service IAM figurant dans votre compte, vous pouvez exécuter la commande `ibmcloud resource service-instances`. 

Les artefacts suivants sont créés conjointement avec votre espace de nom. Ne les supprimez pas. 

* Un ID de service est créé. Il peut être utilisé comme ID fonctionnel lors d'appels sortants. Toutes les actions créées dans cet espace de nom peuvent utiliser cet ID de service pour accéder à d'autres ressources. Pour afficher tous vos ID de service, exécutez la commande `ibmcloud iam service-ids`. 

* Une clé d'API est créée pour l'ID de service ci-dessus, qui peut être utilisé pour générer des jetons IAM. Vous pouvez ensuite utiliser ces jetons pour authentifier l'espace de nom auprès d'autres services IBM Cloud. La clé d'API est fournie aux actions en tant que variable d'environnement. 


## Limitations
{: #limitations}

La [création d'API avec API Gateway](/docs/openwhisk?topic=cloud-functions-openwhisk_apigateway) et l'utilisation du [kit SDK mobile](/docs/openwhisk?topic=cloud-functions-openwhisk_mobile_sdk) ne sont pas prises en compte pour les espaces
de nom IAM pour l'instant. 

</br>

Afin de cibler le service de back end {{site.data.keyword.openwhisk_short}} dans l'emplacement Tokyo, vous devez ajouter `apihost` à tous les appels
d'interface de ligne de commande, par exemple `ibmcloud fn namespace list --apihost jp-tok.functions.cloud.ibm.com`. Cette solution est temporaire jusqu'à
ce que l'emplacement puisse être ciblé par `ibmcloud target -r jp-tok`.
{: tip}



</br>
</br>


## Création d'un espace de nom avec l'interface de ligne de commande
{: #create_iam_cli}

Vous pouvez créer un espace de nom géré par IAM dans le cadre d'un groupe de ressources et gérer les règles d'accès pour vos ressources en ciblant le groupe de ressources lors de la création d'un espace de nom. Si d'autres utilisateurs ont besoin d'accéder à votre espace de nom ou si vous voulez accéder à d'autres ressources à partir des actions de
votre espace de nom, n'oubliez pas de définir des règles IAM après la création de votre espace de nom.
{: shortdesc}

1. Ciblez le groupe de ressources où vous voulez créer l'espace de nom. Si vous n'avez pas encore créé de [groupe de ressources](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_resource#ibmcloud_resource_group_create),
vous pouvez cibler le groupe de ressources par défaut `default`. 

    ```
    ibmcloud target -g default
    ```
    {: pre}

2. Créez un espace de nom activé pour IAM. 

    ```
    ibmcloud fn namespace create <nom_espace de nom> [-n <description>]
    ```
    {: pre}

    <table>
      <thead>
        <tr>
          <th colspan=2><img src="images/idea.png" alt="Icône Idée"/> Description des composants de cette commande</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><code>&lt;nom_espace de nom&gt;</code></td>
          <td>Nom d'affichage pour le nouvel espace de nom IAM. </td>
        </tr>
        <tr>
          <td><code>-n &lt;description&gt;</code></td>
          <td>Facultatif : ajoutez une description à l'espace de nom, comme le type d'actions ou de packages qu'il contiendra. </td>
        </tr>
      </tbody>
    </table>

    Exemple de sortie :
    ```
    ok: created namespace myNamespace
    ```
    {: screen}

3. Vérifiez que votre nouvel espace de nom est créé. 

    ```
    ibmcloud fn namespace get <nom_ou_ID_espace de nom> --no-entities
    ```
    {: pre}

    Exemple de sortie :

    ```
    Details of namespace: 'myNamespace'
    Description: 'short description'
    Resource Plan Id: 'functions-base-plan'
    Location: 'jp-tok'
    ID: '05bae599-ead6-4ccb-9ca3-94ce8c8b3e43'
    ```
    {: screen}

    Vous pouvez également répertorier tous les espaces de nom, notamment les espaces de nom IAM et Cloud Foundry :
    ```
    ibmcloud fn namespace list --iam
    ```
    {: pre}

4. Avant de créer des entités dans le nouvel espace de nom, définissez le contexte de votre interface de ligne de commande sur l'espace de nom en le ciblant.
    ```
    ibmcloud fn property set --namespace <ID_ou_nom_espace de nom>
    ```
    {: pre}

</br>

## Création d'un espace de nom avec l'API
{: #create_iam_api}

Vous pouvez créer un espace de nom géré par IAM dans le cadre d'un groupe de ressources et gérer les règles d'accès pour vos ressources en ciblant le groupe de ressources lors de la création d'un espace de nom. Si d'autres utilisateurs ont besoin d'accéder à votre espace de nom ou si vous voulez accéder à d'autres ressources à partir des actions de
votre espace de nom, n'oubliez pas de définir des règles IAM après la création de votre espace de nom.
{: shortdesc}



2. Créez un espace de nom activé pour IAM. 

    ```
    curl --request POST \
    --url 'https://jp-tok.functions.cloud.ibm.com/api/v1/namespaces \
    --header 'accept: application/json' \
    --header 'authorization: <jeton_IAM>' \
    --data '{"description":"string","name":"string","resource_group_id":"string","resource_plan_id":"string"}'
    ```
    {: pre}

    <table>
      <thead>
        <tr>
          <th colspan=2><img src="images/idea.png" alt="Icône Idée"/> Description des composants de cette commande</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><code>&lt;jeton_IAM&gt;</code></td>
          <td>Votre jeton IBM Cloud Identity and Access Management (IAM). Pour extraire votre jeton IAM, exécutez <code>ibmcloud iam oauth-tokens</code>. </td>
        </tr>
        <tr>
          <td><code>-n &lt;nom&gt;</code></td>
          <td>Nom de l'espace de nom. </td>
        </tr>
        <tr>
          <td><code>-n &lt;ID_groupe_ressources&gt;</code></td>
          <td>ID du groupe de ressources où vous voulez créer l'espace de nom. Pour afficher les ID de groupe de ressources, exécutez <code>ibmcloud resource groups</code>. </td>
        </tr>
        <tr>
          <td><code>-n &lt;ID_plan_ressources&gt;</code></td>
          <td>ID du plan de ressources, comme functions-base-plan</td>
        </tr>
        <tr>
          <td><code>-n &lt;description&gt;</code></td>
          <td>Facultatif : ajoutez une description à l'espace de nom, comme le type d'actions ou de packages qu'il contiendra. </td>
        </tr>
      </tbody>
    </table>

    Exemple de sortie :
    ```
    {
      "description": "Mon nouvel espace de nom pour les packages X, Y et Z.",
      "id": "12345678-1234-abcd-1234-123456789abc",
      "location": "jp-tok",
      "crn": "crn:v1:functions:jp-tok:a/1a22bb3c44dd1a22bb3c44dd1a22:12345678-1234-abcd-1234-123456789abc::",
      "name": "mynamespace",
      "resource_group_id": "1a22bb3c44dd1a22bb3c44dd1a22",
      "resource_plan_id": "functions-base-plan"
    }
    ```
    {: screen}

3. Vérifiez que votre nouvel espace de nom est créé. 

    ```
    curl --request GET \
      --url 'https://us-south.functions.cloud.ibm.com/api/servicebroker/api/v1/namespaces/{id} \
      --header 'accept: application/json' \
      --header 'authorization: <jeton_IAM>'
    ```
    {: pre}

    Vous pouvez également répertorier tous les espaces de nom, notamment les espaces de nom IAM et Cloud Foundry :
    ```
    curl --request GET \
      --url 'https://jp-tok.functions.cloud.ibm.com/api/v1/namespaces?limit=0&offset=0' \
      --header 'accept: application/json' \
      --header 'authorization: <jeton_IAM>'
    ```
    {: pre}

    Exemple de sortie :
    ```
    {
      "limit": 10,
      "offset": 0,
      "total_Count": 2,
      "namespaces": [
        {
          "id": "12345678-1234-abcd-1234-123456789abc",
          "location": "jp-tok"
        },
        {
          "id": "BobsOrg_dev",
          "classic_type": 1,
          "location": "jp-tok"
        }
      ]
    }
    ```
    {: screen}


Pour plus d'informations sur l'utilisation de HTTP REST, consultez la [documentation relative à l'API Cloud Functions](https://cloud.ibm.com/apidocs/functions).
{: tip}

</br>
</br>


## Etapes suivantes
{: #next}

Maintenant que vous avez créé un espace de nom, vous pouvez créer des règles d'accès IAM pour le protéger. Pour commencer, consultez [Gestion des accès](/docs/openwhisk?topic=cloud-functions-iam#iam). Pour plus d'informations sur la gestion des espaces de nom IAM, voir le [{{site.data.keyword.openwhisk_short}}document de référence de l'API REST](https://cloud.ibm.com/apidocs/functions).
