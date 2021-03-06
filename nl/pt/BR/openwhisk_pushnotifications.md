---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-15"

keywords: push notifications, events, parameters, triggers, service activity

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Push móvel em eventos de dispositivo
{: #openwhisk_pushnotifications}

Esse pacote pré-instalado não está disponível na região de Tóquio.
{: tip}

Saiba como configurar o serviço Push para disparar um acionador quando há atividade de dispositivo, como registro/remoção de registro ou assinatura/cancelamento de assinatura do dispositivo em um aplicativo especificado.
{: shortdesc}

Para obter informações sobre o pacote `/whisk.system/pushnotifications` em si, veja o tópico [Push móvel](/docs/services/mobilepush?topic=mobile-pushnotification-push_step_1a#push_step_1a) que cobre a criação de uma ligação de pacote Push e o envio de uma notificação Push.

## Parâmetros de Push
{: #push_notif_parameters}

Os parâmetros de `/whisk.system/pushnotifications/webhook` são os seguintes:
- `appId`: o GUID do app do {{site.data.keyword.Bluemix_notm}}.
- `appSecret`: o serviço de notificação push do {{site.data.keyword.Bluemix_notm}} `appSecret`.
- `events`: `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`

  É possível usar o caractere curinga "`*`" para ser notificado para todos os eventos.

## Disparando um evento acionador na atividade do serviço Push Notifications
{: #trigger_push_notify}

Para criar um acionador que é disparado toda vez que um novo dispositivo é registrado com o aplicativo de serviço de Notificações Push, veja o exemplo a seguir:

1. Crie uma ligação de pacote que seja configurada para o seu serviço Push Notifications usando seu `appId` e `appSecret`.
  ```
  ibmcloud fn package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crie um acionador para o tipo de evento `onDeviceRegister` do serviço de Notificações Push usando seu feed `myPush/webhook`.
  ```
  ibmcloud fn trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}

3. É possível criar uma regra que envia uma mensagem cada vez que um novo dispositivo é registrado. Crie uma regra usando a ação e o acionador anteriores.
  ```
  ibmcloud fn rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}

4. Verifique os resultados usando o comando `ibmcloud fn activation poll`.
  ```
  ibmcloud fn activation poll
  ```
  {: pre}

5. Registre um dispositivo em seu aplicativo {{site.data.keyword.Bluemix_notm}}. É possível ver que `rule`, `trigger` e `action` são executados no painel do {{site.data.keyword.openwhisk}} [](https://cloud.ibm.com/openwhisk/dashboard).

  A ação envia uma notificação Push.
