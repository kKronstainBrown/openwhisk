---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-05"

keywords: functions cli, serverless, bluemix cli, install, functions plug-in

subcollection: cloud-functions

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 设置 {{site.data.keyword.openwhisk_short}} CLI 插件
{: #cloudfunctions_cli}


{{site.data.keyword.openwhisk}} 为 {{site.data.keyword.Bluemix_notm}} CLI 提供了功能强大的插件，支持对 {{site.data.keyword.openwhisk_short}} 系统进行全面管理。
可以使用 {{site.data.keyword.openwhisk_short}} CLI 插件来管理操作中的代码片段，创建触发器和规则以支持操作对事件进行响应以及将操作捆绑到包中。
{:shortdesc}

现在，您可以在 {{site.data.keyword.openwhisk_short}} 插件命令中使用别名 `fn`：`ibmcloud fn <command>`
{: tip}

## 设置 {{site.data.keyword.Bluemix_notm}} CLI
{: #bluemix_cli_setup}

下载并安装 {{site.data.keyword.Bluemix_notm}} CLI，然后登录。
{: shortdesc}

1. 下载并安装 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli)。

2. 登录到 {{site.data.keyword.Bluemix_notm}} CLI。要指定 IBM Cloud 区域，请[包含 API 端点](/docs/openwhisk?topic=cloud-functions-cloudfunctions_regions)。

  ```
  ibmcloud login
  ```
  {: pre}

  可以在登录时使用以下标志来指定组织和空间，以跳过要求提供组织和空间的提示：`ibmcloud login -o <ORG> -s <SPACE>`
  {: tip}

3. 如果未指定组织和空间，请完成运行登录命令后的提示。


## 安装 {{site.data.keyword.openwhisk_short}} 插件
{: #cloudfunctions_plugin_setup}

要使用 {{site.data.keyword.openwhisk_short}}，请下载并安装 CLI 插件。
{: shortdesc}

可以使用该插件来执行以下操作：

* 在 {{site.data.keyword.openwhisk_short}} 上运行代码片段或操作。请参阅[创建和调用操作](/docs/openwhisk?topic=cloud-functions-openwhisk_actions)。
* 使用触发器和规则以支持操作对事件进行响应。请参阅[创建触发器和规则](/docs/openwhisk?topic=cloud-functions-openwhisk_triggers)。
* 了解包如何捆绑操作以及配置外部事件源。请参阅[创建和使用包](/docs/openwhisk?topic=cloud-functions-openwhisk_packages)。
* 浏览包的目录，并通过外部服务（例如，[{{site.data.keyword.cloudant}} 事件源](/docs/openwhisk?topic=cloud-functions-openwhisk_cloudant)）来增强应用程序的功能。

要查看可以使用 {{site.data.keyword.openwhisk_short}} 插件执行的所有操作，请运行不带自变量的 `ibmcloud fn`。
{: tip}

1. 安装 {{site.data.keyword.openwhisk_short}} 插件。
    

  ```
    ibmcloud plugin install cloud-functions
    ```
  {: pre}

2. 验证插件是否已安装。
    

  ```
    ibmcloud plugin list cloud-functions
    ```
  {: pre}

  输出：
  ```
Plugin Name          Version
    Cloud-Functions      1.0.16
    ```
  {: screen}

已有插件，但需要更新？请运行 `ibmcloud plugin update cloud-functions`。
{:tip}



## 通过操作使用服务
{: #binding_services_cli}

{{site.data.keyword.openwhisk_short}} 提供了 `service bind` 命令，使您的 {{site.data.keyword.Bluemix_notm}} 服务凭证在运行时可用于代码。然后，可以使用 `service bind` 命令将任何 {{site.data.keyword.Bluemix_notm}} 服务绑定到 {{site.data.keyword.openwhisk_short}} 中定义的任何操作。

有关如何通过操作使用服务的详细步骤，请参阅[将服务绑定到操作](/docs/openwhisk?topic=cloud-functions-binding_services)。


## 配置 {{site.data.keyword.openwhisk_short}} CLI 以使用 HTTPS 代理
{: #cli_https_proxy}

{{site.data.keyword.openwhisk_short}} CLI 可以设置为使用 HTTPS 代理。要设置 HTTPS 代理，必须创建名为 `HTTPS_PROXY` 的环境变量。该变量必须设置为 HTTPS 代理的地址及其端口，格式如下：`{PROXY IP}:{PROXY PORT}`。



## 切换到不同的区域、组织和空间
{: #region_info}

如果您已经登录，那么可以在 {{site.data.keyword.Bluemix_notm}} CLI 中运行 `ibmcloud target` 命令来切换区域、组织和空间。


要创建和管理实体，必须将名称空间设定为目标。在某些情况下，缺省名称空间可以用下划线 (`_`) 表示，对应于当前设定为目标的基于 Cloud Foundry 的名称空间。

可以通过为每个预生产（编译打包）和生产部署创建空间来处理这些部署。通过创建空间，{{site.data.keyword.openwhisk_short}} 可以具有为您定义的两个不同名称空间。运行 [`ibmcloud iam space-create`](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_account#ibmcloud_account_space_create) 以在您的组织下创建更多空间（例如“staging”和“production”）：

```
ibmcloud iam space-create "staging"
ibmcloud iam space-create "production"
```
{: pre}

{{site.data.keyword.openwhisk_short}} 对名称空间的名称施加了限制。有关更多信息，请参阅[系统详细信息和限制](/docs/openwhisk?topic=cloud-functions-openwhisk_reference#openwhisk_entities)文档。
{: tip}

**警告**：更改组织或空间的名称将基于更改的名称创建新的名称空间。旧名称空间中的实体不会在新名称空间中显示，并且可能会被删除。


## 从 OpenWhisk CLI 迁移到 {{site.data.keyword.openwhisk_short}} CLI 插件
{: #cli_migration}

现在，可以使用 {{site.data.keyword.openwhisk_short}} CLI 插件与 {{site.data.keyword.openwhisk_short}} 实体进行交互。虽然可以继续使用独立 Openwhisk CLI，但此 CLI 不会有 {{site.data.keyword.openwhisk_short}} 支持的最新功能，例如基于 IAM 的名称空间和 `service bind`。
{: shortdesc}

### 命令语法
{: #command_syntax}

除了不再需要的 `wsk bluemix login` 命令外，其他所有 `wsk` 命令的工作方式与使用 `ibmcloud fn` 命令相同。Cloud Functions CLI 插件中命令的所有命令选项和自变量都与 OpenWhisk 独立 CLI 的命令的相同。有关更多信息，请参阅 [Apache OpenWhisk CLI 项目 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/apache/incubator-openwhisk-cli)。

### API 认证和主机
{: #api_authentication}

OpenWhisk CLI 需要配置认证 API 密钥和 API 主机。使用 {{site.data.keyword.openwhisk_short}} CLI 插件时，您无需显式配置 API 密钥和 API 主机。取而代之的是，您可以使用 `ibmcloud login` 登录，然后使用 `ibmcloud target` 命令将您的区域和名称空间设定为目标。登录后，所有命令都以 `ibmcloud fn` 开头。


如果需要将认证 API 密钥用于外部 HTTP 客户机（例如，cURL 或 Postman）中的 {{site.data.keyword.openwhisk_short}}，可以使用以下命令来检索该密钥：

要获取当前 API 密钥，请运行以下命令：
```
ibmcloud fn property get --auth
```
{: pre}

要获取当前 API 主机，请运行以下命令：
```
ibmcloud fn property get --apihost
```
{: pre}

API 密钥是特定于 {{site.data.keyword.openwhisk_short}} CLI 插件设定为目标的每个区域、组织和空间的。
{: tip}

### API 网关认证
{: #apigw_authentication}

OpenWhisk CLI 需要您运行 `wsk bluemix login` 才能配置 API 网关授权，以使用 `wsk api` 命令来管理 API。使用 {{site.data.keyword.openwhisk_short}} CLI 插件后，无需运行 `wsk bluemix login`。取而代之的是，使用 `ibmcloud login` 命令登录到 {{site.data.keyword.Bluemix_notm}} 时，{{site.data.keyword.openwhisk}} 插件会自动利用您当前的登录和目标信息。现在，您可以使用 `ibmcloud fn api` 命令来管理 API。

### 迁移部署脚本
{: #migrating_deploy_scripts}

如果您具有将 OpenWhisk CLI 与 `wsk` 二进制文件一起使用的脚本，那么所有命令的工作方式与使用 `ibmcloud fn` 命令相同。您可以修改脚本以使用 {{site.data.keyword.Bluemix_notm}} CLI 插件，或者创建别名或包装程序，以便使用 `wsk` 的当前命令转换为 `ibmcloud fn`。{{site.data.keyword.Bluemix_notm}} CLI 中的 `ibmcloud login` 和 `ibmcloud target` 命令以无人照管方式工作。在无人照管方式下，可以先配置环境，然后再运行 `ibmcloud fn` 命令来部署和管理 {{site.data.keyword.openwhisk_short}} 实体。





## CLI 版本历史记录
{: #version_history}

版本的历史记录，其中显示了亮点和错误修订。

V1.0.30（2019 年 4 月 3 日）
* 改进了 `service bind` 对 IAM 以及基于组织和空间的服务的处理。
* 针对处理 API 端点 https://cloud.ibm.com，添加了修订。

V1.0.29（2019 年 2 月 6 日）
* 添加了 `deploy` 和 `undeploy` 命令，用于通过清单文件部署或取消部署 Functions 实体的集合。有关更多信息，请参阅[部署](/docs/openwhisk?topic=cloud-functions-deploy#deploy)文档。

V1.0.28（2019 年 1 月 21 日）
* 添加了 `update|delete|get namespace name` 存在多次时的错误消息。

V1.0.27（2018 年 12 月 11 日）
* 添加了 `namespace get` 修订。
* 针对操作为黑匣操作时的 `--save-as`，添加了修订。
* 为 action create 和 action update 命令添加了 `--concurrency` 标志。

V1.0.26（2018 年 11 月 30 日）
* 启用了 `fn property get --auth` 以在新环境中正确返回认证密钥。

V1.0.25（2018 年 11 月 23 日）
* 改进了错误消息结果显示。
* 添加了 `fn namespace get` 修订以正确显示名称空间属性。

1.0.23（2018 年 10 月 15 日）
* 添加了对 ruby (.rb) 操作代码识别的支持。

1.0.22（2018 年 8 月 20 日）
* 添加了 us-east 区域支持。

1.0.21（2018 年 8 月 1 日）
* 别名 `fn` 和 `functions` 现在可用于 {{site.data.keyword.openwhisk_short}} 命令：`ibmcloud fn <command>` 和 `ibmcloud fn <command>`. 此外，您仍可以使用 `ibmcloud wsk <command>`.

1.0.19（2018 年 7 月 2 日）
* 小错误修订和改进。

1.0.18（2018 年 6 月 20 日）
* 针对取消绑定用户提供的服务实例，添加了修订。
* 改进了性能。

1.0.17（2018 年 6 月 12 日）
* 添加了对使用 `ibmcloud cf create-user-provided-service` 命令创建的用户提供的服务实例执行绑定 (`ibmcloud wsk service bind`) 和取消绑定 (`ibmcloud wsk service unbind`) 操作的支持。

1.0.16（2018 年 5 月 24 日）
* 小错误修订和改进。

1.0.15（2018 年 5 月 21 日）
* 小错误修订和改进。

1.0.14（2018 年 5 月 17 日）
* 在组织和空间名称中启用了对 `&` 字符的支持。

1.0.13（2018 年 5 月 7 日）
* 小错误修订和错误处理改进。

1.0.12（2018 年 4 月 30 日）
* {{site.data.keyword.Bluemix_notm}} SDK 更新，以保持 `bx` CLI 兼容性。

1.0.11（2018 年 4 月 23 日）
* 小错误修订和改进。

1.0.10（2018 年 4 月 9 日）
* 向 `ibmcloud wsk action create|update` 命令添加了新的 `--web-secure` 选项，用于保护 Web 操作端点。
* 修正了背靠背路径参数[缺陷](https://github.com/apache/incubator-openwhisk-cli/issues/237)。

1.0.9（2018 年 3 月 16 日）
* 在包级别启用了对服务绑定的支持。

1.0.8（2018 年 2 月 22 日）
* 启用了对 IAM 服务绑定的支持。

1.0.7（2018 年 2 月 2 日）
* 更新了 `ibmcloud wsk api` 以接受路径参数，例如 `/api/{id}`。有关信息，请参阅 [API 网关](/docs/openwhisk?topic=cloud-functions-openwhisk_apigateway)。
* 复原了代理支持。
* 除去了 `swift:3`。

1.0.6（2018 年 1 月 30 日）
* 修正了针对包内操作的 `ibmcloud wsk service bind` 命令的错误。
