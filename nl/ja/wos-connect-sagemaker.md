---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

Python SDK を使用して、機械学習プロバイダーを追加することもできます。 この操作をプログラムで実行する方法については、[Amazon SageMaker 機械学習エンジンのバインド](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)を参照してください。

## Amazon SageMaker サービス・インスタンスの接続
{: #csm-config}

{{site.data.keyword.aios_short}} を、Amazon SageMaker サービス・インスタンスの AI モデルとデプロイメントに接続します。

1. **「構成」**タブで、**「機械学習プロバイダー (Machine learning provider)」**をクリックします。ご使用の環境によっては、以下のプロバイダーの一部が表示されないことがあります。

   ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

1.  **「Amazon SageMaker」**タイルをクリックします。

    ![Amazon SageMaker サービス資格情報の入力](images/connect-sage-cred.png)

1.  資格情報を入力して保存します。

    - アクセス・キー ID: AWS のアクセス・キー ID `aws_access_key_id`。これにより、本人確認を行い、AWS に対する呼び出しを認証および許可します。
    - シークレット・アクセス・キー: AWS のシークレット・アクセス・キー `aws_secret_access_key`。本人確認を行い、AWS に対する呼び出しを認証および許可するためには、これが必要です。
    - 地域: アクセス・キー ID が作成された地域を入力します。 キーが作成された地域にキーは保管され、そこで使用されます。他の地域に転送することはできません。
    - サービス・プロバイダー・インスタンス名: このサービス・プロバイダーに割り当てられている特定の名前。
    - 説明: (オプション) このサービス・プロバイダー・インスタンスの簡単な説明。実動環境とテスト環境を運用している場合、その情報を含めることをお勧めします。

1.  デプロイされているモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択します。

### 次のステップ
{: #csm-next}

{{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。
