---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Microsoft Azure ML Studio フレームワーク
{: #frmwrks-azure}

Microsoft Azure ML Studio を使用して、ペイロード・ロギングとフィードバック・ロギングを実行し、{{site.data.keyword.aios_full}} でパフォーマンスの正確度、実行時のバイアス検出、説明性、および自動バイアス緩和機能を測定することができます。

{{site.data.keyword.aios_full}} では、以下の Microsoft Azure Machine Learning Studio フレームワークが完全にサポートされています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| ネイティブ | 分類 | 構造化 |
| ネイティブ | 回帰 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

## {{site.data.keyword.aios_short}} への Microsoft Azure ML Studio の追加
{: #frmwrks-azure-add}

次のいずれかの方法を使用して、Microsoft Azure ML Studio と連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めて機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。 詳しくは、[Microsoft Azure ML Studio インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。 複数のプロバイダーが必要な場合は、この方法を使用する必要があります。 この操作をプログラムで実行する方法については、[Microsoft Azure 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)を参照してください。


## サンプル・ノートブック
{: #frmwrks-azure-smpl-ntbks}

以下のノートブックは、Microsoft Azure ML Studio と連携する方法を示しています。

- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service model scoring examples](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 詳細
{: #frmwrks-azure-mediumblogs}

-[Monitor Azure machine learning with Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [How does Azure Machine Learning service differ from Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Microsoft Azure ML Studio インスタンスの指定
{: #connect-azure}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Microsoft Azure ML Studio インスタンスの指定です。 Azure ML Studio インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

Python SDK を使用して、機械学習プロバイダーを追加することもできます。 この操作をプログラムで実行する方法については、[Microsoft Azure 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)を参照してください。

### Azure ML Studio Studio インスタンスの接続
{: #ca-connect}

{{site.data.keyword.aios_short}} を、Azure ML Studio インスタンスの AI モデルとデプロイメントに接続します。

1.  ナビゲーション・ペインの**「構成」**タブで**「機械学習プロバイダー (Machine learning providers)」**をクリックします。

    ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

1.  **「機械学習プロバイダーの追加 (Add machine learning provider)」**ボタンをクリックし、**「Microsoft Azure ML Studio」**タイルをクリックします。

    ![Azure ML Studio 資格情報の入力](images/connect-azure-cred.png)

1.  資格情報を入力して保存します。

    - クライアント ID: クライアント ID の実際の文字列値。これにより、本人確認を行い、Azure Studio に対する呼び出しを認証および許可します。
    - クライアント・シークレット: シークレットの実際の文字列値。これにより、本人確認を行い、Azure Studio に対する呼び出しを認証および許可します。
    - テナント: テナント ID は、組織に対応する Azure AD の専用インスタンスです。テナント ID を確認するには、アカウント名の上にカーソルを置いてディレクトリー/テナント ID を表示するか、Azure ポータルで「Azure Active Directory」>「プロパティ」>「ディレクトリ ID」の順に選択します。
    - サブスクリプション ID: Microsoft Azure サブスクリプションを一意に識別するサブスクリプション資格情報。すべてのサービス呼び出しの URI に、このサブスクリプション ID が含まれます。

    Microsoft Azure 資格情報の取得方法の手順に関しては、[How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} を参照してください。
    {: note}

1.  デプロイされているモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択して**「構成」**をクリックします。

デプロイメントが正常に選択されました。

## Microsoft Azure Machine Learning Studio エンジンのペイロード・ロギング
{: #cml-azconfig}

### Microsoft Azure Machine Learning エンジンのバインド
{: #cml-azbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML バインディング](images/ml-azure-bind.png)

### Microsoft Azure ML Studio サブスクリプションの追加
{: #cml-azsub}

- サブスクリプションを追加します

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### ペイロード・ロギングの有効化
{: #cml-azenlog}

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### 評価とペイロード・ロギング
{: #cml-azscore}

- モデルを評価します。 完全なサンプルについては、[Azure Machine Learning Studio エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}を参照してください。

- ペイロード・ロギング・テーブルにリクエストと応答を格納します。

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用してペイロード・ロギングを直接実行することもできます。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```


## 次のステップ
{: #ca-next}

{{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。
