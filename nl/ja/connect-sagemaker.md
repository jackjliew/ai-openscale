---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Amazon SageMaker, machine learning, services, AWS

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Amazon SageMaker ML サービス・インスタンスの指定
{: #csm-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Amazon SageMaker サービス・インスタンスの指定です。 Amazon SageMaker サービス・インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## Amazon SageMaker サービス・インスタンスの接続
{: #csm-config}

{{site.data.keyword.aios_short}} を、Amazon SageMaker サービス・インスタンスの AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「Amazon SageMaker」**タイルを選択し、**「次へ」**をクリックします。

    ![Amazon SageMaker サービスの選択](images/connect-sage.png)

1.  資格情報を入力します。

    ![Amazon SageMaker サービス資格情報の入力](images/connect-sage-cred.png)

1.  **「次へ」**をクリックします。

1.  {{site.data.keyword.aios_short}} によって、デプロイ済みモデルがリストされるので、モニター対象となるモデルを選択します

    ![Amazon SageMaker デプロイ済みモデルの選択](images/connect-sage-deploys.png)

1.  **「次へ」**をクリックします。

### 次のステップ
{: #csm-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db)準備が整いました。
