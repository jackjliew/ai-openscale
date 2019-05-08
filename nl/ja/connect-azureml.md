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

# Microsoft Azure ML サービス・インスタンスの指定
{: #caz-connect}

{{site.data.keyword.aios_short}} ツールでの最初の手順は、Microsoft Azure ML サービス・インスタンスの指定です。Azure ML サービス・インスタンスに AI モデルとデプロイメントが保管されます。
{: shortdesc}

## Azure ML Studio サービス・インスタンスの接続
{: #caz-config}

{{site.data.keyword.aios_short}} は、Azure ML Studio サービス・インスタンス内の AI モデルとデプロイメントに接続します。

1.  {{site.data.keyword.aios_short}} ツールのホーム・ページから、**「開始 (Begin)」**をクリックします。

    ![ホーム・ページ](images/gs-config-start.png)

1.  **「Microsoft Azure ML Studio」**タイルを選択し、**「次へ」**をクリックします。

    ![Azure ML サービスの選択](images/connect-azure.png)

1.  以下のように、資格情報を入力します。

    Microsoft Azure 資格情報の取得方法に関する指示については、[方法:リソースにアクセスできる Azure AD アプリケーションとサービス プリンシパルをポータルで作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} を参照してください。
    {: note}

    ![Azure ML サービス資格情報の入力](images/connect-azure-cred.png)

1.  **「次へ」**をクリックします。

1.  デプロイされたモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択します。

    ![MS Azure のデプロイ済みモデルの選択](images/connect-azure-deploys.png)

1.  **「次へ」**をクリックします。

## 次のステップ
{: #caz-next}

{{site.data.keyword.aios_short}} で[データベースを指定](ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)する準備ができました。
