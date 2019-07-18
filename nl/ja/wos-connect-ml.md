---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} サービス以外のインスタンスのペイロード・ロギング
{: #cml-connect}

AI モデルを {{site.data.keyword.pm_full}} 以外の機械学習エンジンでデプロイしている場合、Python クライアントを使用して外部機械学習エンジンのペイロード・ロギングを有効にする必要があります。
{: shortdesc}

さらに詳しい情報については、[{{site.data.keyword.aios_short}} Python クライアント資料](http://ai-openscale-python-client.mybluemix.net/){: external}、および [{{site.data.keyword.aios_short}} チュートリアル](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}に含まれているサンプル {{site.data.keyword.aios_short}} Python クライアント・ノートブックを参照してください。

## 始めに
{: #cml-prereq}

モデルのバイアスをモニターするためには、Db2 または {{site.data.keyword.cos_full}} でモデルの訓練データが利用できる状態になっている必要があります。 Python 関数では説明性と正解率はサポートされていません。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。

- {{site.data.keyword.aios_short}} をインポートして開始します

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  資格情報は、「[資格情報の作成](/docs/services/ai-openscale?topic=ai-openscale-cred-create)」トピックに示されているステップに従って確認できます。

- PostgreSQL データベースでスキーマ名を作成します

- データマートをセットアップします

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## 次のステップ
{: #cml-next}

- {{site.data.keyword.aios_short}} クライアントを使用して作業を続けるには、[正解率モニターまたはモデル性能モニターの構成](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)を参照してください。
- Python コマンド・ライブラリーを使用して作業を続けるには、[Python クライアント資料](http://ai-openscale-python-client.mybluemix.net/){: external}を参照してください。
