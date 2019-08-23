---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# 指定資料庫
{: #connect-db}

指定資料庫以供 {{site.data.keyword.aios_short}} 實例使用。
{: shortdesc}

## 連接至資料庫
{: #cdb-connect}

{{site.data.keyword.aios_short}} 使用資料庫來儲存有效負載、回饋資料和測量資料。除了選取資料庫，您也可以選取資料庫的綱目 - 綱目是資料庫中一個已命名的表格集合。

1.  選擇資料庫。您有兩個選項：免費資料庫，或是現有資料庫或新的資料庫。

    ![會顯示「選取您的資料庫」畫面，其中提供兩個選項，以便選擇要使用免費 Lite 方案，還是使用現有的資料庫](images/gs-config-database.png)

    如果您已有一個付費 {{site.data.keyword.cloud_notm}} 帳戶，您可以佈建 `Databases for PostgreSQL` 或 `Db2 Warehouse` 服務，以便充分利用與 Watson Studio 和持續學習服務的整合。如果您選擇不佈建付費服務，您可以將免費的內部 PostgreSQL 儲存空間與 {{site.data.keyword.aios_short}} 搭配使用，只是這就無法為模型配置持續學習。
    {: note}

### 免費 Lite 方案資料庫
{: #cdb-lite}

**附註**：免費資料庫有一些重要限制：

- 免費資料庫是代管的，您無法直接存取。
- {{site.data.keyword.aios_full}} 對您的資料庫具備完整存取權，因此也對您的資料具備完整存取權。
- 免費資料庫不符合 GDPR 標準。如果您的模型會處理個人識別資訊 (PII)，就無法使用免費資料庫。您必須購買新的資料庫，或是使用符合 GDPR 規則的現有資料庫。請參閱[資訊安全](/docs/services/ai-openscale?topic=ai-openscale-is-ov)，以進一步瞭解。

若要繼續使用免費資料庫，請按一下**使用免費 Lite 方案資料庫**圖磚，然後按一下**儲存**。

  ![會顯示「資料庫已儲存」蹦現訊息，其中已選取「選取提供者」按鈕](images/gs-config-database2.png)
  
您可以從免費資料庫升級至另一個資料庫，但是無法將 Compose for Postgres、Database for Postgres 或 Db2 實例重新配置到免費資料庫。升級之後，就無法回去使用免費資料庫。您將無法重複使用所有現行資料，例如配置、評分結果和說明。透過選取另一個綱目或資料庫，將 {{site.data.keyword.aios_short}} 環境完全重設。



### 現有或新的資料庫
{: #cdb-exn}

1.  選取**使用現有資料庫或購買新資料庫**選項之後，{{site.data.keyword.aios_short}} 會檢查您的 {{site.data.keyword.Bluemix_notm}} 帳戶，以找出任何現有的資料庫。

1.  選取您現有的資料庫類型（Compose for Postgres、Database for Postgres 或 Db2）、從**資料庫**下拉功能表中選取一個資料庫，然後選取一項**綱目**：

    {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 資料庫，來儲存模型相關資料（回饋資料、評分有效負載）和計算後的度量。目前不支援 Lite Db2 方案。如需訓練資料的相關資訊，請參閱[為何 {{site.data.keyword.aios_short}} 需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![會顯示「選取資料庫」畫面，其中具有一些欄位，供您輸入資料庫類型、資料庫名稱和綱目。](images/gs-config-database3.png)

1.  您也可以按一下**選取不同位置**，以指定一個位於您 {{site.data.keyword.Bluemix_notm}} 帳戶之外的資料庫位置。

    {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 資料庫，來儲存模型相關資料（回饋資料、評分有效負載）和計算後的度量。目前不支援 Lite Db2 方案。{: note}

    - 選取**資料庫類型**（`Compose for PostgreSQL`、`Database for PostgreSQL` 或 `Db2`），然後提供連線資訊：

        - 若為 `Compose for PostgreSQL` 資料庫，請完成下列項目：

            - 主機名稱或 IP 位址
            - 埠
            - 資料庫（名稱）
            - 使用者名稱
            - 密碼

        - 若為 `Database for PostgreSQL` 資料庫，請完成下列項目：

            - 主機名稱或 IP 位址
            - SSL 埠
            - Base-64 編碼憑證
            - 資料庫（名稱）
            - 使用者名稱
            - 密碼

        - 若為 `Db2` 資料庫，請完成下列項目：

            - 主機名稱或 IP 位址
            - SSL 埠
            - 資料庫（名稱）
            - 使用者名稱
            - 密碼

    - 順利連接之後，您可以選取綱目，並儲存您的工作。

      如果您所提供的 Db2 實例具有存取上的限制，而不容許自動產生綱目名稱，則需要明確提供綱目名稱。這適用於「入門 Db2 Warehouse」方案。{: important}

## 後續步驟
{: #cdb-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[傳送評分有效負載](/docs/services/ai-openscale?topic=ai-openscale-cdb-score)以及[配置部署的監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
