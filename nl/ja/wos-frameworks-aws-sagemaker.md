---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker フレームワーク
{: #frmwrks-aws-sage}

Amazon SageMaker を使用して、ペイロード・ロギングとフィードバック・ロギングを実行し、{{site.data.keyword.aios_full}} でパフォーマンスの正確度、実行時のバイアス検出、説明性、および自動バイアス緩和機能を測定することができます。

{{site.data.keyword.aios_full}} では、以下の Amazon SageMaker フレームワークが完全にサポートされています。
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| ネイティブ | 分類 | 構造化 |
| ネイティブ | 回帰<sup>1</sup> | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

<sup>1</sup> 回帰モデルのサポートにはドリフト絶対値は含まれません。

## {{site.data.keyword.aios_short}} への Amazon SageMaker の追加
{: #frmwrks-aws-sage-add}

次のいずれかの方法を使用して、Amazon SageMaker と連携するように {{site.data.keyword.aios_short}} を構成できます。

- 初めて機械学習プロバイダーを {{site.data.keyword.aios_short}} に追加する場合は、構成インターフェースを使用すると良いでしょう。 詳しくは、[Amazon SageMaker インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)を参照してください。
- Python SDK を使用して、機械学習プロバイダーを追加することもできます。 複数のプロバイダーが必要な場合は、この方法を使用する必要があります。 この操作をプログラムで実行する方法については、[Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)を参照してください。


## サンプル・ノートブック
{: #frmwrks-aws-sage-smpl-ntbks}

以下のノートブックは、Amazon SageMaker と連携する方法を示しています。

- [信用リスク予測モデルの作成とデプロイメント](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [データマートの作成、モデル・デプロイメントのモニター、およびデータ分析](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Amazon SageMaker ML サービス・インスタンスの指定
{: #csm-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Amazon SageMaker サービス・インスタンスの指定です。 Amazon SageMaker サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

Python SDK を使用して、機械学習プロバイダーを追加することもできます。 この操作をプログラムで実行する方法については、[Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)を参照してください。

### Amazon SageMaker サービス・インスタンスの接続
{: #csm-config}

{{site.data.keyword.aios_short}} を、Amazon SageMaker サービス・インスタンスの AI モデルとデプロイメントに接続します。

1.  ナビゲーション・ペインの**「構成」**タブで**「機械学習プロバイダー (Machine learning providers)」**をクリックします。

    ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

1.  **「機械学習プロバイダーの追加 (Add machine learning provider)」**ボタンをクリックし、**「Amazon SageMaker」**タイルをクリックします。

    ![Amazon SageMaker サービス資格情報の入力](images/connect-sage-cred.png)

1.  資格情報を入力して保存します。

    - アクセス・キー ID: AWS のアクセス・キー ID `aws_access_key_id`。これにより、本人確認を行い、AWS に対する呼び出しを認証および許可します。
    - シークレット・アクセス・キー: AWS のシークレット・アクセス・キー `aws_secret_access_key`。本人確認を行い、AWS に対する呼び出しを認証および許可するためには、これが必要です。
    - 地域: アクセス・キー ID が作成された地域を入力します。キーが作成された地域にキーは保管され、そこで使用されます。他の地域に転送することはできません。

1.  デプロイされているモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択します。

## Amazon SageMaker 機械学習エンジンのペイロード・ロギング
{: #cml-smconfig}

### Amazon SageMaker 機械学習エンジンのバインド
{: #cml-smbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML バインディング](images/ml-sagemaker-bind.png)

### Amazon SageMaker ML サブスクリプションの追加
{: #cml-smsub}

- サブスクリプションを追加します

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
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
{: #cml-smenlog}

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### 評価とペイロード・ロギング
{: #cml-smscore}

- モデルを評価します。 完全なサンプルについては、[SageMaker 機械学習エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}を参照してください。


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
{: #csm-next}

- {{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。
- [Monitor Sagemaker machine learning with Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
