---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Watson Machine Learning サービス・インスタンスの指定
{: #wml-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Watson Machine Learning (WML) インスタンスの指定です。WML インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## 前提条件
{: #wml-prereq}

WML インスタンスを、{{site.data.keyword.aios_short}} サービス・インスタンスが配置されている {{site.data.keyword.Bluemix_notm}} アカウントと同じアカウントでプロビジョンしておく必要があります。他のアカウントで WML インスタンスをプロビジョンした場合、そのインスタンスを {{site.data.keyword.aios_short}} で構成することはできません。

## Watson Machine Learning サービス・インスタンスの接続
{: #wml-config}

{{site.data.keyword.aios_short}} を、WML インスタンスの AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

2.  「Watson Machine Learning」タイルを選択します。

    ![タイルの選択](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} によって {{site.data.keyword.Bluemix_notm}} アカウントが検査され、既存の WML インスタンスが検出されます。次に、**「Watson Machine Learning service」**ドロップダウン・メニューからインスタンスを選択できます。

    ![WML サービスの選択](images/gs-set-wml.png)

4.  (オプション)**「Select a different location」**を選択し、ご使用の {{site.data.keyword.Bluemix_notm}} アカウント以外の機械学習の場所を指定することもできます。ご使用の場所の資格情報を有効な JSON として指定します。

    ![WML インスタンスの設定](images/gs-get-wml.png)

    **「次へ」**をクリックします。

5.  {{site.data.keyword.aios_short}} によって、選択した Machine Learning インスタンスが検査され、対象インスタンスに格納されているデプロイメントのリストが検出されます。デプロイメント・リストから、モニターするデプロイメントを選択します。

    ![デプロイメントの選択](images/gs-config-deploy.png)

6.  **「次へ」**をクリックします。
7.  **「保存」**をクリックします。

### 次のステップ
{: #wml-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db)準備が整いました。
