---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-05"

keywords: logging, monitoring, viewing, logs, query, performance, dashboard, metrics, health

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Activité de journalisation et de surveillance
{: #openwhisk_logs}

La journalisation et la surveillance sont automatiquement activés dans {{site.data.keyword.openwhisk}} pour vous aider à résoudre les problèmes et améliorer l'intégrité et les performances de vos actions. Vous pouvez également utiliser le service {{site.data.keyword.cloudaccesstraillong}} pour suivre la façon dont les utilisateurs et les applications interagissent avec le service {{site.data.keyword.openwhisk_short}}. 

## Affichage des journaux
{: #view-logs}

Vous pouvez consulter les journaux d'activation directement depuis le tableau de bord de surveillance {{site.data.keyword.openwhisk_short}}. Les journaux sont également transférés à [{{site.data.keyword.loganalysisfull}}](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana) où ils sont indexés, afin de permettre une recherche en texte intégral à l'aide de tous les messages générés et d'une interrogation efficace basée sur des zones spécifiques.
{:shortdesc}

**Remarque** : la journalisation n'est pas disponible pour la région Est des Etats-Unis. 

1. Affichez la page de surveillance [{{site.data.keyword.openwhisk_short}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/dashboard).

2. Facultatif : pour consulter uniquement les journaux relatifs à une action spécifique, limitez le récapitulatif de surveillance à cette action. Dans la section Options de filtrage, sélectionnez le nom de l'action dans la liste déroulante **Limiter à**.

3. Dans le volet de navigation gauche, cliquez sr **Journaux**. La page {{site.data.keyword.loganalysisshort_notm}} Kibana s'affiche.

4. Facultatif : pour afficher des journaux plus anciens, définissez la valeur de période par défaut sur 15 minutes en cliquant sur **15 dernières minutes** dans l'angle supérieur droit et en sélectionnant une période différente.

### Interrogation des journaux
{: #query-logs}

Vous pouvez trouver des journaux d'activation spécifiques dans [{{site.data.keyword.loganalysislong_notm}}](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana) à l'aide de la syntaxe de requête de Kibana.

Les exemples de requête suivants peuvent vous aider à déboguer des erreurs :
  * Rechercher tous journaux des erreurs :
      ```
      type: user_logs AND stream_str: stderr
      ```
      {: codeblock}

  * Rechercher tous mes journaux des erreurs qui sont générés par "myAction" :
      ```
      type: user_logs AND stream_str: stderr AND action_str: "*myAction"
      ```
      {: codeblock}

### Interrogation des résultats
{: #query-results}

Outre les lignes de journaux, [{{site.data.keyword.loganalysislong_notm}}](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analyzing_logs_Kibana#analyzing_logs_Kibana) indexe également les résultats, ou les enregistrements d'activation, qui sont générés par {{site.data.keyword.openwhisk_short}}. Les résultats contiennent les métadonnées d'activation comme la durée d'activation ou le code de résultat d'activation. L'interrogation des zones de résultat peut vous aider à comprendre le comportement de vos actions {{site.data.keyword.openwhisk_short}}.

Vous pouvez trouver des journaux d'activation spécifiques à l'aide de la syntaxe de requête de Kibana. Les exemples de requête suivants peuvent vous aider à déboguer des erreurs :

* Rechercher toutes les activations ayant échoué :
    ```
    type: activation_record AND NOT status_str: 0
    ```
    {: codeblock}
    Dans les résultats, un `0` indique une action fermée avec succès et toutes les autres valeurs indiquent une erreur.

* Rechercher toutes les activations ayant échoué avec une erreur spécifique :
    ```
    type: activation_record AND NOT status_str:0 AND message: "*VerySpecificErrorMessage*"
    ```
    {: codeblock}


## Surveillance des performances des actions
{: #monitoring_performance}

Vous pouvez obtenir des informations sur les performances de vos actions déployées avec {{site.data.keyword.openwhisk}}. Les métriques peuvent vous aider à détecter des goulots d'étranglement ou à prévoir les éventuels problèmes de production d'après la durée de l'action et les résultats des activations d'action, ou à déterminer lorsque vous avez atteint les limites d'activation d'action.
{: shortdesc}

Les métriques sont collectées automatiquement pour toutes les entités. Selon que vos actions se trouvent dans un espace de nom IAM ou Cloud Foundry, les métriques sont situées dans le compte ou l'espace IBM Cloud. Ces métriques sont envoyées à {{site.data.keyword.monitoringlong}} et mises à disposition via Grafana, où vous pouvez configurer vos tableaux de bord, créer des alertes basées sur les valeurs d'événement des métriques, etc. Pour plus d'informations sur les métriques, consultez la [documentation {{site.data.keyword.monitoringlong_notm}}](/docs/services/cloud-monitoring?topic=cloud-monitoring-getting-started-with-ibm-cloud-monitoring). 

### Création d'un tableau de bord
{: #create_dashboard}

Commencez par créer un tableau de bord de surveillance Grafana. 

1. Accédez à l'une des adresses URL suivantes. 
  <table>
    <thead>
      <tr>
        <th>Région {{site.data.keyword.openwhisk_short}}</th>
        <th>Adresse de surveillance</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Europe centrale</td>
        <td>metrics.eu-de.bluemix.net</td>
      </tr>
      <tr>
        <td>Sud du Royaume-Uni</td>
        <td>metrics.eu-gb.bluemix.net</td>
      </tr>
      <tr>
        <td>Sud des Etats-Unis</td>
        <td>metrics.ng.bluemix.net</td>
      </tr>
      <tr>
        <td>Est des Etats-Unis</td>
        <td>Non disponible</td>
      </tr>
    </tbody>
  </table>

2. Sélectionnez le domaine des métriques. 
    * Espaces de nom IAM : 
        1. Cliquez sur votre nom d'utilisateur. 
        2. Dans la liste déroulante **Domaine**, sélectionnez **compte**. 
        3. Dans la liste déroulante **Compte**, sélectionnez le compte IBM Cloud où se trouve votre espace de nom IAM. 
    * Espaces de nom Cloud Foundry : 
        1. Cliquez sur votre nom d'utilisateur. 
        2. Dans la liste déroulante **Domaine**, sélectionnez **espace**. 
        3. Utilisez les listes déroulantes **Organisation** et **Espace** pour sélectionner votre espace de nom Cloud Foundry. 

3. Créez un tableau de bord. 
    * Pour utiliser le tableau de bord {{site.data.keyword.openwhisk_short}} prédéfini : 
        1. Accédez à **Accueil > Importer**. 
        3. Entrez l'ID du tableau de bord {{site.data.keyword.openwhisk_short}} prédéfini, à savoir `8124`, dans la zone **Tableau de bord Grafana.net**. 
        4. Cliquez sur **Importer**. 
    * Pour créer un tableau de bord personnalisé, accédez à **Accueil > Nouveau**. 

Une fois qu'une action est exécutée, de nouvelles métriques sont générées et peuvent faire l'objet d'une recherche dans Grafana. Remarque : l'affichage de l'action exécutée dans Grafana peut prendre jusqu'à 10 minutes. 


### Format de métrique
{: #metric_format}

Les métriques reflètent les données collectées à partir de vos activations d'action, qui sont agrégées par minute. Les métriques sont consultables au niveau d'accès concurrent ou de performance de l'action. 


**Métriques de performance de l'action**

Les métriques de performance d'une action sont des valeurs calculées pour une action unique. Elles comprennent à la fois les caractéristiques de temps des exécutions et le statut des activations. Remarque : si vous n'indiquez pas le nom d'un package lors de sa création, le nom du package par défaut est utilisé. Ces métriques sont au format suivant : 

```
ibmcloud.public.functions.<région>.action.namespace.<espace de nom>.<package>.<action>.<nom_métrique>
```
{: codeblock}

Les caractères suivants sont convertis en tirets (`-`) : point (.), arobase (@), blanc ( ), perluète (&), trait de soulignement (_), deux-points (:)
{: tip}

Exemple : si une action nommée `hello-world` se trouve dans l'espace de nom Cloud Foundry `user@email.com_dev` dans la région `us-south`, une métrique de performance d'action se présente comme suit : 

```
ibmcloud.public.functions.us-south.action.namespace.user-ibm-com-dev.action-performance.default.hello-world.duration
```
{: screen}

</br>

**Métriques d'accès concurrent d'une action**

Les métriques d'accès concurrent d'une action sont calculées à partir des données provenant de toutes les actions actives dans un espace de nom. L'accès concurrent d'une action inclut le nombre d'appels simultanés et les régulateurs système qui peuvent éventuellement survenir en cas de dépassement des limites d'accès concurrent. Ces métriques sont au format suivant : 

```
ibmcloud.public.functions.<région>.action.namespace.<espace de nom>.action-performance.<package>.<action>.<nom_métrique>
```
{: codeblock}

Exemple : si un espace de nom IAM nommé `myNamespace` se trouve dans la région `us-south`, une métrique d'accès concurrent d'une action se présente comme suit : 

```
ibmcloud.public.functions.us-south.action.namespace.all.concurrent-invocations
```
{: screen}

</br>

**Métriques disponibles**

Etant donné qu'il peut exister des milliers ou millions d'activations d'action, les valeurs de métrique sont représentées sous forme d'agrégation d'événements générés par de nombreuses activations. Les valeurs sont agrégées de la manière suivante :
* Somme : toutes les valeurs de métrique sont additionnées. 
* Moyenne : une moyenne arithmétique est calculée. 
* Somme moyenne : une moyenne arithmétique est calculée en fonction des composants et en ajoutant les différents composants. 

Consultez le tableau suivant pour savoir quelles métriques sont à votre disposition. 

<table>
  <thead>
    <tr>
      <th>Nom de métrique</th>
      <th>Description</th>
      <th>Type</th>
      <th>Catégorie</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>duration</code></td>
      <td>Durée moyenne d'une action, durée d'exécution de l'action facturée. </td>
      <td>Moyenne</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>init-time</code></td>
      <td>Temps passé à initialiser le conteneur d'action.</td>
      <td>Moyenne</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>wait-time</code></td>
      <td>Temps moyen passé dans une file d'attente à attendre la planification d'une activation. </td>
      <td>Moyenne</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>activation</code></td>
      <td>Nombre total d'activations qui ont été déclenchées dans le système.</td>
      <td>Somme</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>status.success</code></td>
      <td>Nombre d'activations réussies du code d'action.</td>
      <td>Somme</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>status.error.application</code></td>
      <td>Nombre d'échecs d'activations provoqués par des erreurs d'application. Par exemple, erreurs correctes provenant des actions. Pour plus d'informations sur la façon dont les métriques action-performance sont dérivées, consultez [Understanding the activation record](https://github.com/apache/incubator-openwhisk/blob/master/docs/actions.md#understanding-the-activation-record). </td>
      <td>Somme</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>status.error.developer</code></td>
      <td>Nombre d'échecs d'activations provoqués par le développeur. Par exemple, la violation de l'[interface proxy de l'action](https://github.com/apache/incubator-openwhisk/blob/master/docs/actions-new.md#action-interface) par des exceptions non gérées dans le code d'action. </td>
      <td>Somme</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>status.error.internal</code></td>
      <td>Nombre d'échecs d'activations provoqués par des erreurs internes {{site.data.keyword.openwhisk_short}}. </td>
      <td>Somme</td>
      <td><code>action-performance</code></td>
    </tr>
    <tr>
      <td><code>concurrent-rate-limit</code></td>
      <td>Somme des activations régulées en raison du dépassement de la limite de débit d'accès concurrent. Aucune métrique n'est émise si la limite n'est pas atteinte. </td>
      <td>Somme</td>
      <td><code>action-concurrency</code></td>
    </tr>
    <tr>
      <td><code>timed-rate-limit</code></td>
      <td>Somme des activations régulées en raison du dépassement de la limite par minute. Aucune métrique n'est émise si la limite n'est pas atteinte. </td>
      <td>Somme</td>
      <td><code>action-concurrency</code></td>
    </tr>
    <tr>
      <td><code>concurrent-invocations</code></td>
      <td>Nombre d'appels simultanés dans le système.</td>
      <td>Somme moyenne</td>
      <td><code>action-concurrency</code></td>
    </tr>
  </tbody>
</table>

Les métriques pour les actions qui existent dans le cadre d'un espace de nom par défaut sont disponibles dans la catégorie par défaut.
{: tip}



## Surveillance de la santé des actions
{: #openwhisk_monitoring}

Le [tableau de bord {{site.data.keyword.openwhisk_short}}](https://cloud.ibm.com/openwhisk/dashboard) fournit un récapitulatif graphique de votre activité. Utilisez-le pour déterminer les performances et la santé de vos actions {{site.data.keyword.openwhisk_short}}.
{:shortdesc}

Vous pouvez filtrer les journaux en sélectionnant les journaux d'actions que vous souhaitez afficher et la période d'activité consignée. Ces filtres sont appliqués à toutes les vues du tableau de bord. Cliquez sur **Rechargement** à tout moment pour mettre à jour le tableau de bord avec les données de journal d'activation les plus récentes.

### Récapitulatif de l'activité
{: #activity_summary}

La vue **Activity Summary** fournit un récapitulatif général de votre environnement {{site.data.keyword.openwhisk_short}}. Utilisez cette vue pour surveiller la santé et les performances générales de votre service activé pour {{site.data.keyword.openwhisk_short}}. A partir des métriques affichées dans cette vue, vous pouvez :
* Déterminer la fréquence d'utilisation des actions compatibles avec {{site.data.keyword.openwhisk_short}} de votre service en affichant le
nombre de fois qu'elles ont été appelées.
* Déterminer le taux d'échec global pour toutes les actions. Si vous détectez une erreur, vous pouvez déterminer quels sont les services ou quelles sont les actions qui présentent des erreurs en affichant la vue de l'**histogramme de l'activité**. Isolez les erreurs proprement dites en affichant le **journal d'activité**.
* Déterminer si vos actions s'exécutent correctement en affichant le temps d'exécution moyen associé à chaque action.

### Chronologie de l'activité
{: #timeline}

La vue de la **chronologie de l'activité** affiche un graphique à barres verticales qui présente l'activité des actions passées et présentes. Le rouge indique des erreurs dans des actions spécifiques. Corrélez cette vue avec le **journal d'activité** pour plus de détails sur les erreurs.



### Journal d'activité
{: #log}

Cette vue **Journal d'activité** affiche une version formatée du journal d'activation. Elle affiche les détails de chaque activation et recherche les nouvelles activations toutes les minutes. Cliquez sur une action pour afficher un journal détaillé.

Pour obtenir la sortie affichée dans le journal d'activité via l'interface de ligne de commande, utilisez la commande suivante :
```
ibmcloud fn activation poll
```
{: pre}
