---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} サービス・インスタンスの指定
{: #wml-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、{{site.data.keyword.pm_full}} インスタンスの指定です。 {{site.data.keyword.pm_short}} インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## 前提条件
{: #wml-prereq}

{{site.data.keyword.pm_full}} インスタンスを、{{site.data.keyword.aios_short}} サービス・インスタンスが配置されている {{site.data.keyword.Bluemix_notm}} アカウントと同じアカウントでプロビジョンしておく必要があります。 他のアカウントで {{site.data.keyword.pm_full}} インスタンスをプロビジョンした場合、そのインスタンスには {{site.data.keyword.aios_short}} の自動ペイロード・ロギングは構成できません。

## {{site.data.keyword.pm_short}} サービス・インスタンスの接続
{: #wml-config}

{{site.data.keyword.aios_short}} は、{{site.data.keyword.pm_full}} インスタンス内の AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

2.  {{site.data.keyword.pm_full}} タイルを選択します。

    ![タイルの選択](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} は、ご使用の {{site.data.keyword.Bluemix_notm}} アカウントを調べて、既存の {{site.data.keyword.pm_full}} インスタンスを見つけます。 次に、**「Watson Machine Learning service」**ドロップダウン・メニューからインスタンスを選択できます。

    ![{{site.data.keyword.pm_short}} サービスの選択](images/gs-set-wml.png)

4.  (オプション)**「別の場所を選択」**を選択し、ご使用の {{site.data.keyword.Bluemix_notm}} アカウント以外の機械学習の場所を指定することもできます。 ご使用の場所の資格情報を有効な JSON として指定します。

    ![{{site.data.keyword.pm_short}} インスタンスの設定](images/gs-get-wml.png)

    **「次へ」**をクリックします。

5.  {{site.data.keyword.aios_short}} によって、選択した Machine Learning インスタンスが検査され、対象インスタンスに格納されているデプロイメントのリストが検出されます。 デプロイメント・リストから、モニターするデプロイメントを選択します。

    ![デプロイメントの選択](images/gs-config-deploy.png)

6.  **「次へ」**をクリックします。
7.  **「保存」**をクリックします。

### 次のステップ
{: #wml-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db)準備が整いました。
