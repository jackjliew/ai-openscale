---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 建立認證
{: #cred-create}

若要存取 {{site.data.keyword.aios_short}} REST API，則需要「平台 API 金鑰」和資料集區（服務實例）ID。「平台 API 金鑰」可讓個別使用者能夠存取 {{site.data.keyword.cloud_notm}} 中的資源。

對於企業帳戶，管理者可以建立資料集區，然後邀請其他使用者加入該帳戶，以便提供特定 {{site.data.keyword.aios_short}} 資料集區的存取權給那些使用者。之後使用者就可以建立自己的「平台 API 金鑰」，並且可以存取相同的 {{site.data.keyword.aios_short}} 資料集區；這不會有任何的衝突或安全風險。

如果要建立「平台 API 金鑰」，請完成下列步驟：

- 登入 [{{site.data.keyword.cloud_notm}} ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}){: new_window}。

- 選取**管理** --> **安全** --> **平台 API 金鑰**

    ![平台 API 金鑰](images/cred-api-key.png)

- 建立並儲存「平台 API 金鑰」。

如果要尋找資料集區（或服務實例）ID，請執行下列動作：

- 在 {{site.data.keyword.aios_short}} **配置 --> 摘要**頁面中，第一筆項目是您的資料集區（服務實例）ID。

    ![資料集區 ID](images/data-mart-id.png)
