---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-05"

keywords: deploy, deployment templates, templates, example, quickstart

subcollection: cloud-functions

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Déploiement de modèles Quickstart
{: #serviceauth}

{{site.data.keyword.openwhisk}} offre un catalogue de modèles destinés à vous permettre de commencer rapidement à travailler sur votre nouveau projet. Les modèles représentent une combinaison d'actions, de déclencheurs et de séquences. Certains modèles incorporent également d'autres instances de service provenant d'{{site.data.keyword.Bluemix_notm}}. Les modèles vous permettent de créer rapidement et facilement un projet et de commencer immédiatement le codage.
{: shortdesc}

## Modèles Quickstart disponibles
{: #available-templates}

| Nom | Description | Environnements d'exécution pris en charge |
|:-----------------|:-----------------|:-----------------|
| [{{site.data.keyword.cloudant_short_notm}} Events](/docs/openwhisk?topic=cloud-functions-serviceauth#cloudant-template) | Lorsqu'un document est édité ou ajouté dans une base de données {{site.data.keyword.cloudantfull}}, la modification est consignée dans la console. | Node.js, Swift, Python, PHP |
| [Upload Image](/docs/openwhisk?topic=cloud-functions-serviceauth#cos-upload-image) | Utilisez une action Web pour envoyer par téléchargement une image vers le compartiment d'une instance {{site.data.keyword.cos_full}}, puis extraire une miniature de cette image. | Node.js |
| [Get HTTP Resource](/docs/openwhisk?topic=cloud-functions-serviceauth#get-http-resource-template) | Appelez une action Web à l'aide d'un événement HTTP et accédez aux données de l'API Yahoo Weather. | Node.js, Python |
| [Hello World](/docs/openwhisk?topic=cloud-functions-serviceauth#hello-world-template) | Créez une action de base qui accepte un objet JSON en tant que paramètre unique. | Node.js, Swift, Python, PHP |
| [{{site.data.keyword.messagehub}} Events](/docs/openwhisk?topic=cloud-functions-serviceauth#messagehub-events-template) | Lorsque de nouvelles données sont ajoutées dans une rubrique {{site.data.keyword.messagehub_full}}, la modification est consignée dans la console. | Node.js, Swift, Python, PHP |
| [Periodic Slack Reminder](/docs/openwhisk?topic=cloud-functions-serviceauth#slack-reminder-template) | Utilisez un webhook dans Slack en fonction d'un déclencheur périodique. | Node.js, Swift, Python, PHP |

## Déploiement du modèle {{site.data.keyword.cloudant_short_notm}} Events
{: #cloudant-template}

Le modèle {{site.data.keyword.cloudant_short_notm}} crée une séquence d'actions et un déclencheur qui lance cette séquence. Le déclencheur est lancé lorsqu'une modification est apportée à l'exemple de base de données de chats {{site.data.keyword.cloudant_short_notm}} connectée. L'élément de données attendu est un chat portant le nom et la couleur définis. Lorsqu'un nouveau chat est ajouté à la base de données ou qu'un chat en cours est édité, les données sont consignées sur la console.

### Déploiement du modèle {{site.data.keyword.cloudant_short_notm}} Events à partir de l'interface utilisateur

1. Accédez à la [page Create ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Cloudant Events**.

4. Créez l'action {{site.data.keyword.cloudant_short_notm}}. 
    1. Entrez un nom pour votre package ou utilisez le nom fourni par défaut, `new-cloudant-item`.
    2. Dans la liste **Actions**, sélectionnez `Node.js 6` pour l'exemple de base de données de chats et cliquez sur **Suivant**. 

5. Créez le déclencheur {{site.data.keyword.cloudant_short_notm}}. Les déclencheurs appellent des actions lorsqu'ils reçoivent des événements de la part de sources d'événements externes. Pour créer le déclencheur, vous devez fournir une instance de service {{site.data.keyword.messagehub}} et les données d'identification du service. 
    1. Dans la liste **Instance Cloudant**, sélectionnez **Créez votre instance**. La page de configuration {{site.data.keyword.cloudant_short_notm}} s'affiche. 
    2. Créez l'instance de service {{site.data.keyword.cloudant_short_notm}}. 
    3. Créez un ensemble de données d'identification pour le service. 
    4. Cliquez sur **OK** pour fermer la page de configuration {{site.data.keyword.cloudant_short_notm}} et revenir à la console {{site.data.keyword.openwhisk_short}}. 
    5. Dans la liste **Instance Cloudant**, vous pouvez maintenant choisir **Entrez vos propres données d'identification** et indiquer les informations suivantes : 
      * Utilisateur : Votre nom d'utilisateur {{site.data.keyword.cloudant_short_notm}}
      * Mot de passe : Votre mot de passe {{site.data.keyword.cloudant_short_notm}}
      * Hôte : `<username>.cloudant.com`
      * Base de données : Nom de votre base de données {{site.data.keyword.cloudant_short_notm}}

5. Cliquez sur **Déployer**. Une fois le déploiement du modèle terminé, vous pouvez apporter d'autres modifications au code afin de le personnaliser en fonction de vos besoins, ou revenir en arrière et vérifier le catalogue de modèles disponibles.

### Déploiement du modèle {{site.data.keyword.cloudant_short_notm}} Events à partir de l'interface de ligne de commande

1. Clonez le référentiel de modèle.
    ```
    git clone https://github.com/ibm-functions/template-cloudant-trigger.git
    ```
    {: pre}

2. Accédez au répertoire du contexte d'exécution d'action que vous souhaitez utiliser : `nodejs-6`, `nodejs`, `php`, `python` ou `swift`.
    ```
    cd template-cloudant-trigger/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle, en utilisant les variables d'environnement suivantes :
    ```
    CLOUDANT_HOSTNAME=<hôte> CLOUDANT_USERNAME=<nom d'utilisateur> CLOUDANT_PASSWORD=<mot de passe> CLOUDANT_DATABASE=<base de données> PACKAGE_NAME=<nom> RULE_NAME=<nom> TRIGGER_NAME=<nom> ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

    <table>
    <caption>Présentation des variables d'environnement</caption>
    <thead>
    <th colspan=2>Présentation des variables d'environnement</th>
    </thead>
    <tbody>
    <tr><td><code>CLOUDANT_HOSTNAME</code></td><td><code>&lt;nom d'utilisateur&gt;.cloudant.com</code></td></tr>
    <tr><td><code>CLOUDANT_USERNAME</code></td><td>Votre nom d'utilisateur {{site.data.keyword.cloudant_short_notm}}</td></tr>
    <tr><td><code>CLOUDANT_PASSWORD</code></td><td>Votre mot de passe {{site.data.keyword.cloudant_short_notm}}</td></tr>
    <tr><td><code>CLOUDANT_DATABASE</code></td><td>Nom de votre base de données {{site.data.keyword.cloudant_short_notm}}</td></tr>
    <tr><td><code>PACKAGE_NAME</code></td><td>Un nom personnalisé pour le package</td></tr>
    <tr><td><code>RULE_NAME</code></td><td>Un nom personnalisé pour la règle</td></tr>
    <tr><td><code>TRIGGER_NAME</code></td><td>Un nom personnalisé pour le déclencheur</td></tr>
    </tbody></table>

## Déploiement du modèle Télécharger une image
{: #cos-upload-image}

Le modèle Télécharger une image crée une action Web qui vous permet d'envoyer par téléchargement une image à un compartiment {{site.data.keyword.cos_short}} via une petite interface. Le modèle extrait ensuite l'image sous la forme d'une miniature et l'affiche dans l'interface de l'action Web.

### Déploiement du modèle Télécharger une image à partir de l'interface utilisateur

1. Accédez à la [page Créer ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Télécharger une image**. 

4. Entrez un nom pour votre package ou utilisez le nom par défaut `upload-image`, puis cliquez sur **Suivant**. 

6. Le modèle requiert les données d'identification du service d'une instance de service {{site.data.keyword.cos_full_notm}}. Dans la liste **{{site.data.keyword.cos_short}}**,
sélectionnez l'une des options suivantes :
  * **Créez une nouvelle instance** : si vous n'avez pas d'instance de service, sélectionnez cette option pour en créer une.
      1. Dans la page de création d'instance de service de {{site.data.keyword.cos_full_notm}} qui s'affiche, créez une instance de service.
      2. [Créez un ensemble de données d'identification du service HMAC](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials).
      3. [Créez au moins un compartiment](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started-tutorial#gs-create-buckets).
  * **Entrez vos propres données d'identification** : sélectionnez cette option pour saisir manuellement vos propres données d'identification pour une instance de service {{site.data.keyword.cos_short}}. Les données d'identification doivent contenir des clés HMAC et l'instance de service doit avoir au moins un compartiment.
  * **Instances existantes** : si vous avez des instances {{site.data.keyword.cos_short}}, sélectionnez-en une dans la liste. Les données d'identification doivent contenir des clés HMAC et l'instance de service doit avoir au moins un compartiment.

7. Cliquez sur **Déployer**.

8. Dans le volet de navigation gauche, cliquez sur **Noeuds finaux**.

9. Dans la section **Action Web**, copiez le lien sans le suffixe .json et collez-le dans la barre d'adresse de votre navigateur. L'interface de l'action Web du modèle s'affiche.

10. Facultatif : une fois le modèle déployé, vous pouvez accéder au tableau de bord **Actions** afin de personnaliser le code dans les deux nouveaux packages :
    * Le package `cloud-object-storage`, qui contient les actions compatibles avec les instances {{site.data.keyword.cos_short}}
    * Le package de modèle (nom par défaut `upload-image`), qui contient l'action `app`

### Déploiement du modèle Télécharger une image à partir de l'interface de ligne de commande

1. [Installez le package {{site.data.keyword.cos_full_notm}}](/docs/openwhisk?topic=cloud-functions-cloud_object_storage_actions#cloud_object_storage_cli). 

2. Clonez le référentiel de modèle.
    ```
    git clone https://github.com/ibm-functions/template-cloud-object-storage.git
    ```
    {: pre}

3. Accédez au répertoire d'exécution `nodejs`.
    ```
    cd template-cloud-object-storage/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle, en utilisant un nom de package personnalisé et le nom de votre compartiment {{site.data.keyword.cos_short}} comme variables d'environnement.
    ```
    PACKAGE_NAME=<nom> BUCKET_NAME=<nom> ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

4. Dans la [page Actions ![Icône de lienexterne](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/actions) de la console {{site.data.keyword.openwhisk_short}}, cliquez sur l'action `process-change`. 


5. Dans le volet de navigation gauche, cliquez sur **Noeuds finaux**. 

6. Dans la section **Action Web**, copiez le lien sans le suffixe .json et collez-le dans la barre d'adresse de votre navigateur. L'interface de l'action Web du modèle s'affiche.

## Déploiement du modèle Get HTTP Resource
{: #get-http-resource-template}

Le modèle Get HTTP Resource crée une action permettant d'extraire une ressource externe, l'API Yahoo Weather, puis renvoie des données. Cette action est activée en tant qu'action web, ce qui lui permet d'être appelée avec une adresse URL compatible avec CORS sans avoir besoin de clé d'authentification, ce qui est pratique pour générer des système de back end pour les applications Web. **Remarque** : par défaut, le noeud final `get-http-resource` est disponible publiquement pour toutes les personnes qui l'appellent. 

### Déploiement du modèle Get HTTP Resource à partir de l'interface utilisateur

1. Accédez à la [page Créer ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Get HTTP Resource**. 

3. Entrez un nom pour votre package ou utilisez le nom par défaut `get-http-resource`.

4. Choisissez l'environnement d'exécution de vos actions : Node.js 8, Node.js 6 ou Python 3. 

5. Cliquez sur **Déployer**.

6. Appelez l'action en lançant l'utilitaire curl à l'URL suivante : `https://us-south.functions.cloud.ibm.com/api/v1/web/<namespace>/$PACKAGE_NAME/weather?location=<city>`. Par exemple :
    ```
    curl https://us-south.functions.cloud.ibm.com/api/v1/web/myusername@email.com_myspace/Get%20Resource/weather?location=Austin
    ```
    {: pre}

Une fois le déploiement du modèle terminé, vous pouvez apporter d'autres modifications au code afin de le personnaliser en fonction de vos besoins, ou revenir en arrière et vérifier le catalogue de modèles disponibles.

### Déploiement du modèle Get HTTP Resource à partir de l'interface de ligne de commande

1. Clonez le référentiel de modèle.
    ```
    git clone https://github.com/ibm-functions/template-get-external-resource.git
    ```
    {: pre}

2. Accédez au répertoire du contexte d'exécution d'action que vous souhaitez utiliser : `nodejs-6`, `nodejs` ou `python`.
    ```
    cd template-get-external-resource/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle, en utilisant un nom de package personnalisé comme variable d'environnement.
    ```
    PACKAGE_NAME=<nom> ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

4. Appelez l'action en lançant l'utilitaire curl à l'URL suivante : `https://us-south.functions.cloud.ibm.com/api/v1/web/<namespace>/$PACKAGE_NAME/weather?location=<city>`. Par exemple :
    ```
    curl https://us-south.functions.cloud.ibm.com/api/v1/web/myusername@email.com_myspace/Get%20Resource/weather?location=Austin
    ```
    {: pre}

## Déploiement du modèle Hello World
{: #hello-world-template}

Vous pouvez déployer cette action de base Hello World pour vous initier à {{site.data.keyword.openwhisk_short}} ou pour tester d'autres entités que vous créez, comme des déclencheurs et des règles. 

### Déploiement du modèle Hello World à partir de l'interface utilisateur

1. Accédez à la [page Créer ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Hello World**. 

4. Entrez un nom pour votre package ou utilisez le nom par défaut `hello-world`.

5. Choisissez l'environnement d'exécution de vos actions : Node.js 8, Node.js 6, Python 3, Swift 4 ou PHP 7.1. 

6. Cliquez sur **Déployer**.

Une fois le déploiement du modèle terminé, vous pouvez apporter d'autres modifications au code afin de le personnaliser en fonction de vos besoins, ou revenir en arrière et vérifier le catalogue de modèles disponibles.

### Déploiement du modèle Hello World à partir de l'interface de ligne de commande

1. Clonez le référentiel de modèle Hello World.
    ```
    git clone https://github.com/ibm-functions/template-hello-world.git
    ```
    {: pre}

2. Accédez au répertoire du contexte d'exécution d'action que vous souhaitez utiliser : `nodejs-6`, `nodejs`, `php`, `python` ou `swift`.
    ```
    cd template-hello-world/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle.
    ```
    ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

## Déploiement du modèle {{site.data.keyword.messagehub}} Events
{: #messagehub-events-template}

Le modèle {{site.data.keyword.messagehub}} Events crée une action et un déclencheur pour la lancer. Le déclencheur s'exécute chaque fois qu'un nouvel élément est ajouté dans la rubrique {{site.data.keyword.messagehub}} sélectionnée lors de la création du modèle.

### Déploiement du modèle {{site.data.keyword.messagehub}} Events à partir de l'interface utilisateur

1. Accédez à la [page Créer ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Evénements {{site.data.keyword.messagehub}}**. 

4. Créez l'action {{site.data.keyword.messagehub}}. 
    1. Entrez un nom pour votre package ou utilisez le nom fourni par défaut, `message-hub-events`.
    2. Choisissez l'environnement d'exécution de vos actions : Node.js 8, Node.js 6, Python 3, Swift 4 ou PHP 7.1. 
    3. Cliquez sur **Suivant**.

5. Créez le déclencheur {{site.data.keyword.messagehub}}. Les déclencheurs appellent des actions lorsqu'ils reçoivent des événements de la part de sources d'événements externes. Pour créer le déclencheur, vous devez fournir une instance de service {{site.data.keyword.messagehub}} et les données d'identification du service. 
    1. Dans la liste **Instance MessageHub**, sélectionnez **Créez votre instance**. La page de création {{site.data.keyword.messagehub}} s'affiche. 
    2. Créez l'instance de service {{site.data.keyword.messagehub}}. 
    3. Créez un ensemble de données d'identification pour le service. 
    4. Cliquez sur **OK** pour fermer la page de création {{site.data.keyword.messagehub}} et revenir à la console {{site.data.keyword.messagehub}}. 
    5. Dans la liste **Instance MessageHub**, vous pouvez maintenant choisir **Entrez vos propres données d'identification** et indiquer les informations suivantes : 
      * Utilisateur : Votre nom d'utilisateur {{site.data.keyword.messagehub}}
      * Mot de passe : Votre mot de passe {{site.data.keyword.messagehub}}
      * url_admin_kafka : Votre adresse URL REST d'administration {{site.data.keyword.messagehub}}
      * Base de données : Nom de votre base de données {{site.data.keyword.messagehub}}
      * Rubrique : Rubrique à laquelle s'abonner

5. Cliquez sur **Déployer**.

Une fois le déploiement du modèle terminé, vous pouvez apporter d'autres modifications au code afin de le personnaliser en fonction de vos besoins, ou revenir en arrière et vérifier le catalogue de modèles disponibles.

### Déploiement du modèle {{site.data.keyword.messagehub}} Events à partir de l'interface de ligne de commande

1. Clonez le référentiel de modèle.
    ```
    git clone https://github.com/ibm-functions/template-messagehub-trigger.git
    ```
    {: pre}

2. Accédez au répertoire du contexte d'exécution d'action que vous souhaitez utiliser : `nodejs-6`, `nodejs`, `php`, `python` ou `swift`.
    ```
    cd template-messagehub-trigger/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle, en utilisant les variables d'environnement suivantes :
    ```
    KAFKA_BROKERS=<hôte> KAFKA_TOPIC=<rubrique> MESSAGEHUB_USER=<nom d'utilisateur> MESSAGEHUB_PASS=<mot de passe> PACKAGE_NAME=<nom> RULE_NAME=<nom> TRIGGER_NAME=<nom> ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

    <table>
    <caption>Présentation des variables d'environnement</caption>
    <thead>
    <th colspan=2>Présentation des variables d'environnement</th>
    </thead>
    <tbody>
    <tr><td><code>KAFKA_BROKERS</code></td><td>Votre adresse URL REST d'administration {{site.data.keyword.messagehub}}</td></tr>
    <tr><td><code>KAFKA_TOPIC</code></td><td>Rubrique à laquelle s'abonner</td></tr>
    <tr><td><code>MESSAGEHUB_USER</code></td><td>Votre nom d'utilisateur {{site.data.keyword.messagehub}}</td></tr>
    <tr><td><code>MESSAGEHUB_PASS</code></td><td>Votre mot de passe {{site.data.keyword.messagehub}}</td></tr>
    <tr><td><code>PACKAGE_NAME</code></td><td>Un nom personnalisé pour le package</td></tr>
    <tr><td><code>RULE_NAME</code></td><td>Un nom personnalisé pour la règle</td></tr>
    <tr><td><code>TRIGGER_NAME</code></td><td>Un nom personnalisé pour le déclencheur</td></tr>
    </tbody></table>

## Déploiement du modèle Periodic Slack Reminder
{: #slack-reminder-template}

Le modèle Periodic Slack Reminder publie dans Slack en fonction d'un intervalle fourni par l'utilisateur lors de la création du déclencheur.

### Déploiement du modèle Periodic Slack Reminder à partir de l'interface utilisateur

1. Accédez à https://api.slack.com/incoming-webhooks pour configurer l'adresse URL des webhooks entrants requis. 

1. Accédez à la [page Créer ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/openwhisk/create) dans la console {{site.data.keyword.openwhisk_short}}. 

2. Cliquez sur **Modèles Quickstart**.

3. Cliquez sur **Evénements Periodic Slack Reminder**. 

4. Créez l'action Periodic Slack Reminder. 
    1. Entrez un nom pour votre package ou utilisez le nom fourni par défaut, `periodic-slack-reminder`.
    2. Choisissez l'environnement d'exécution de vos actions : Node.js 8, Node.js 6, Python 3, Swift 4 ou PHP 7.1. 
    3. Dans la section Paramètres, entrez l'URL du webhook dans la zone **Valeur du paramètre**, comme `https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX`. 
    4. Cliquez sur **Suivant**.

5. Créez le déclencheur Periodic Slack Reminder. Les déclencheurs appellent des actions lorsqu'ils reçoivent des événements de la part de sources d'événements externes. 
    1. Spécifiez l'intervalle de temps du déclencheur à l'aide d'une expression Modèle ou Cron. 
        * Modèle : Sélectionnez des heures de temps universel coordonné pour les jours de la semaine, les heures et les minutes. 
        * Cron : Spécifiez une séquence Cron basée sur la <a href="http://crontab.org">syntaxe UNIX crontab</a>. Utilisez au maximum 5 zones séparées par des espaces au format `X X X X X`. 
    2. Ajoutez le contenu JSON du déclencheur. 

6. Cliquez sur **Déployer**.

Une fois le déploiement du modèle terminé, vous pouvez apporter d'autres modifications au code afin de le personnaliser en fonction de vos besoins, ou revenir en arrière et vérifier le catalogue de modèles disponibles.

### Déploiement du modèle Periodic Slack Reminder à partir de l'interface de ligne de commande

1. Accédez à https://api.slack.com/incoming-webhooks pour configurer l'adresse URL des webhooks entrants requis. 

1. Clonez le référentiel de modèle.
    ```
    git clone https://github.com/ibm-functions/template-reminder-slack.git
    ```
    {: pre}

2. Accédez au répertoire du contexte d'exécution d'action que vous souhaitez utiliser : `nodejs-6`, `nodejs`, `php`, `python` ou `swift`.
    ```
    cd template-reminder-slack/runtimes/nodejs
    ```
    {: pre}

3. Déployez le modèle, en utilisant les variables d'environnement suivantes :
    ```
    SLACK_WEBHOOK_URL=<url> ALARM_CRON=<cron> PACKAGE_NAME=<nom> RULE_NAME=<nom> TRIGGER_NAME=<nom> ibmcloud fn deploy -m manifest.yaml
    ```
    {: pre}

    <table>
    <caption>Présentation des variables d'environnement</caption>
    <thead>
    <th colspan=2>Présentation des variables d'environnement</th>
    </thead>
    <tbody>
    <tr><td><code>SLACK_WEBHOOK_URL</code></td><td>URL de webhook, comme <code>https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX</code></td></tr>
    <tr><td><code>ALARM_CRON</code></td><td>Séquence Cron basée sur la <a href="http://crontab.org">syntaxe UNIX crontab</a>. Utilisez au maximum 5 zones séparées par des espaces au format <code>X X X X X</code>. </td></tr>
    <tr><td><code>PACKAGE_NAME</code></td><td>Un nom personnalisé pour le package</td></tr>
    <tr><td><code>RULE_NAME</code></td><td>Un nom personnalisé pour la règle</td></tr>
    <tr><td><code>TRIGGER_NAME</code></td><td>Un nom personnalisé pour le déclencheur</td></tr>
    </tbody></table>
