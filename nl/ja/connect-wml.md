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

# Watson Machine Learning サービス・インスタンスの指定
{: #cwml-wml}

{{site.data.keyword.aios_short}} ツールでの最初の手順は、Watson Machine Learning (WML) インスタンスの指定です。WML インスタンスに AI モデルとデプロイメントが保管されます。
{: shortdesc}

## 前提条件
{: #cwml-prereq}

WML インスタンスは、{{site.data.keyword.aios_short}} サービス・インスタンスがあるのと同じ {{site.data.keyword.cloud_notm}} アカウントにプロビジョンしておく必要があります。WML を別のアカウントにプロビジョンした場合、そのインスタンスを {{site.data.keyword.aios_short}} で構成することはできません。

## Watson Machine Learning サービス・インスタンスの接続
{: #cwml-config}

{{site.data.keyword.aios_short}} は、WML インスタンス内の AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページから、**「開始 (Begin)」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  「Watson Machine Learning」タイルを選択して、**「次へ」**をクリックします。

    ![タイルの選択](images/connect-wml.png)

1.  {{site.data.keyword.aios_short}} は、ご使用の {{site.data.keyword.cloud_notm}} アカウントを調べて、既存の WML インスタンスを見つけます。その後で、**「Watson Machine Learning サービス (Watson Machine Learning service)」**ドロップダウン・メニューからインスタンスを選択できます。

    ![WML サービスの選択](images/gs-set-wml.png)

1.  (オプション) オプションとして、**別のロケーションを選択し**、自分の {{site.data.keyword.cloud_notm}} アカウント以外の機械学習ロケーションを指定することもできます。以下のように、ご使用のロケーションの資格情報を有効な JSON として指定します。

    ![WML インスタンスの設定](images/gs-get-wml.png)

    **「次へ」**をクリックします。

1.  {{site.data.keyword.aios_short}} は、選択した Machine Learning インスタンスを調べて、そのインスタンスに保管されているデプロイメントのリストを見つけます。デプロイメントのリストから、モニター対象を選択します。

    ![デプロイメントの選択](images/gs-config-deploy.png)

1.  **「次へ」**をクリックします。
1.  **「保存」**をクリックします。

### 次のステップ
{: #connect-next}

{{site.data.keyword.aios_short}} で[データベースを指定](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)する準備ができました。
