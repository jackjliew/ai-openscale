---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Amazon SageMaker ML サービス・インスタンスの指定
{: #csm-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Amazon SageMaker サービス・インスタンスの指定です。 Amazon SageMaker サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

Python SDK を使用して、機械学習プロバイダーを追加することもできます。この操作をプログラムで実行する方法については、[Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)を参照してください。

## Amazon SageMaker サービス・インスタンスの接続
{: #csm-config}

{{site.data.keyword.aios_short}} を、Amazon SageMaker サービス・インスタンスの AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「Amazon SageMaker」**タイルを選択し、**「次へ」**をクリックします。

    ![Amazon SageMaker サービスの選択](images/connect-sage.png)

1.  資格情報を入力します。

    - アクセス・キー ID: AWS のアクセス・キー ID `aws_access_key_id`。これにより、本人確認を行い、AWS に対する呼び出しを認証および許可します。
    - シークレット・アクセス・キー: AWS のシークレット・アクセス・キー `aws_secret_access_key`。本人確認を行い、AWS に対する呼び出しを認証および許可するためには、これが必要です。
    - 地域: アクセス・キー ID が作成された地域を入力します。キーが作成された地域にキーは保管され、そこで使用されます。他の地域に転送することはできません。

    ![Amazon SageMaker サービス資格情報の入力](images/connect-sage-cred.png)

1.  **「次へ」**をクリックします。

1.  {{site.data.keyword.aios_short}} によって、デプロイ済みモデルがリストされるので、モニター対象となるモデルを選択します

    ![Amazon SageMaker デプロイ済みモデルの選択](images/connect-sage-deploys.png)

1.  **「次へ」**をクリックします。

### 次のステップ
{: #csm-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db)準備が整いました。
