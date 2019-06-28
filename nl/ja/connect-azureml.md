---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure, ml, machine learning, services

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

# Microsoft Azure ML Studio インスタンスの指定
{: #connect-azure}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、Microsoft Azure ML Studio インスタンスの指定です。 Azure ML Studio インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

## Azure ML Studio Studio インスタンスの接続
{: #ca-connect}

{{site.data.keyword.aios_short}} を、Azure ML Studio インスタンスの AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページで、**「開始」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「Microsoft Azure ML Studio」**タイルを選択し、**「次へ」**をクリックします。

    ![Azure ML Studio の選択](images/connect-azure.png)

1.  資格情報を入力します。

    Microsoft Azure 資格情報の取得方法の手順に関しては、[方法:リソースにアクセスできる Azure AD アプリケーションとサービス プリンシパルをポータルで作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} を参照してください。
    {: note}

    ![Azure ML Studio 資格情報の入力](images/connect-azure-cred.png)

1.  **「次へ」**をクリックします。

1.  {{site.data.keyword.aios_short}} によって、デプロイ済みモデルがリストされるので、モニター対象となるモデルを選択します

    ![MS Azure デプロイ済みモデルの選択](images/connect-azure-deploys.png)

1.  **「次へ」**をクリックします。

### 次のステップ
{: #ca-next}

{{site.data.keyword.aios_short}} で[データベースを指定する](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db)準備が整いました。
