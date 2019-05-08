---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 資格情報の作成
{: #cred-creds}

{{site.data.keyword.aios_short}} の資格情報を作成するには、{{site.data.keyword.cloud_notm}} [コマンド・コンソール](/docs/cli?topic=cloud-cli-ibmcloud-cli)を使用して、以下の手順を実行します。

- API 鍵を取得します。

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    次のような情報の出力が表示されます。

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```
- 自分の {{site.data.keyword.cloud_notm}} アカウントで使用しているリソース・グループを確認します。

  ![クラウド内のリソース・グループ](images/cloud-resource.png)

  `デフォルト`のリソース・グループを使用していない場合は、次のコマンドを実行して、{{site.data.keyword.aios_short}} の資格情報を取得します。

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  ここで、`myResourceGroup` は、{{site.data.keyword.aios_short}} インスタンスに関連付けられているリソース・グループの名前です。

- {{site.data.keyword.aios_short}} インスタンス ID を取得します。

    ```curl
    ibmcloud resource service-instance '<Your_AI_OpenScale_instance_name>'
    ```
    **注:** Windows で {{site.data.keyword.cloud_notm}} コマンド・コンソールを使用している場合は、上記のコマンドの単一引用符 (') を二重引用符 (") に置き換えてください。

    次のような情報の出力が表示されます。

    ```bash
    Name:                  AI OpenScale-my_instance
    ID:                    crn:v1:bluemix:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Location:              us-south
    Service Name:          aiopenscale
    Service Plan Name:     lite
    Resource Group Name:   Default
    State:                 active
    Type:                  service_instance
    Sub Type:
    Tags:
    Created at:            2018-09-17T13:58:43Z
    Updated at:
    ```

    `GUID` の値は、ご使用の {{site.data.keyword.aios_short}} インスタンス ID です。
