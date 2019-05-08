---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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
{: #csage-sagemaker}

{{site.data.keyword.aios_short}} ツールでの最初の手順は、Amazon SageMaker サービス・インスタンスの指定です。Amazon SageMaker サービス・インスタンスに AI モデルとデプロイメントが保管されます。
{: shortdesc}

## Amazon SageMaker サービス・インスタンスの接続
{: #csage-config}

{{site.data.keyword.aios_short}} は、Amazon SageMaker サービス・インスタンス内の AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページから、**「開始 (Begin)」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「Amazon SageMaker」**タイルを選択し、**「次へ」**をクリックします。

    ![Amazon SageMaker サービスの選択](images/connect-sage.png)

1.  以下のように、資格情報を入力します。

    ![Amazon SageMaker サービス資格情報の入力](images/connect-sage-cred.png)

1.  **「次へ」**をクリックします。

1.  デプロイされたモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択します。

    ![Amazon SageMaker のデプロイ済みモデルの選択](images/connect-sage-deploys.png)

1.  **「次へ」**をクリックします。

## 次のステップ
{: #csage-next}

{{site.data.keyword.aios_short}} で[データベースを指定](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)する準備ができました。
