---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# 互動式設置指導教學
{: #gs-obj}

在本指導教學中，您將學習如何佈建必要的 {{site.data.keyword.Bluemix_notm}} 服務、設置專案並在 Watson Studio 中部署範例模型，以及在 {{site.data.keyword.aios_short}} 中配置監視器。
{: shortdesc}

1. [佈建 {{site.data.keyword.Bluemix_notm}} 機器學習和儲存服務](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps)。
2. [設置一個 Watson Studio 專案，並建立、訓練及部署機器學習模型](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup)。
3. [配置及探索您模型的信任、透明度和可解釋性](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios)。

## 佈建 {{site.data.keyword.Bluemix_notm}} 必備服務
{: #gs-prps}

除了 {{site.data.keyword.aios_short}}，如果要完成本指導教學，您需要具備下列帳戶和服務。

**重要事項**：為求最佳效能，建議將必備服務建立在與 {{site.data.keyword.aios_short}} 相同的地區中。如果要檢視 {{site.data.keyword.aios_short}} 的可用位置，請參閱[服務可用性](/docs/resources?topic=resources-services_region){: external}。

1.  使用您的 {{site.data.keyword.ibmid}}，登入 [{{site.data.keyword.Bluemix_notm}} 帳戶](https://{DomainName}){: external}。
1.  對於尚未與您帳戶相關聯的下列每一項服務，請按一下此鏈結，為服務命名，選取 **Lite**（免費）方案，並按一下**建立**按鈕，來建立一個實例：

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## 設置 Watson Studio 專案
{: #gs-setup}

1.  登入 [Watson Studio 帳戶](https://dataplatform.ibm.com/){: external}，並從建立新專案開始。按一下**建立專案**。

    ![Watson Studio - 建立專案](images/studio_create_proj.png)

1.  按一下**建立空專案**圖磚。
1.  為專案提供名稱和說明，在**儲存空間**功能表中，確定已選取您在先前步驟中建立的 Object Storage 服務，並按一下**建立**。

### 使您的 {{site.data.keyword.Bluemix_notm}} 服務與 Watson 專案產生關聯
{: #gs-assoc}

1.  開啟 Watson Studio 專案，並選取**設定**標籤。在**相關聯的服務**區段中，按一下**新增服務**，然後按一下 **Watson**。

    ![新增 Watson 服務](images/add_watson_service.png)

1.  按一下**機器學習**圖磚上的**新增**鏈結。
2.  在**現有**標籤上，從**現有服務實例**下拉清單中，按一下您先前建立的服務。
3. 按一下**選取**。

### 新增 `Credit Risk` 模型
{: #gs-addmod}

1.  在 {{site.data.keyword.DSX}} 中，選取您專案的**資產**標籤，捲動至 **Watson Machine Learning 模型**區段，並按一下**新建 Watson Machine Learning 模型**按鈕。


1.  從**選取模型類型**區段中，選取**從樣本**和 `Credit Risk` 模型，然後按一下**建立**。


    ![顯示 Credit Risk 圖磚](images/credit-sample-model.png)

### 部署 `Credit Risk` 模型
{: #gs-depmod}

1.  從 `Credit Risk` 模型頁面，按一下**部署**標籤，然後按一下**新增部署**。
1.  輸入 `credit-risk-deploy` 作為部署名稱，並選取 **Web 服務**部署類型。
1.  按一下**儲存**。

## 配置 {{site.data.keyword.aios_short}}
{: #gs-confaios}

到目前為止，機器學習模型已部署，您可以配置 {{site.data.keyword.aios_short}}，以確保您的模型具備可信任性與透明度。


### 佈建 {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [佈建新的 {{site.data.keyword.aios_short}} 服務實例](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  為您的服務命名，選取 **Lite 方案**，並按一下**建立**。

1.  選取您 {{site.data.keyword.aios_short}} 實例的**管理**標籤，並按一下**啟動應用程式**按鈕。會開啟**歡迎使用 {{site.data.keyword.aios_short}}** 示範頁面。
2. 對於本指導教學，請按一下**否，謝謝**。

### 選取資料庫
{: #gs-db-choice}

接下來，您需要選擇資料庫。您有兩個選項：免費資料庫，或是現有資料庫或新的資料庫。

2. 對於本指導教學，請選取**使用免費 Lite 方案資料庫**圖磚。

   免費資料庫有一些重要限制。它是一個代管資料庫，並未給予您個別存取權。它讓 {{site.data.keyword.aios_short}} 能夠存取您的資料庫和資料。它不符合 GDPR 標準。有關每一個選項的更多完整詳細資料，請參閱[指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)主題。現有的資料庫可以是 PostgreSQL 資料庫或 Db2 資料庫。
    {: tip}

   ![選取資料庫](images/gs-set-lite-db2.png)

1.  檢閱摘要資料，並按一下**儲存**。當確認並出現提示時，請按一下**繼續配置**按鈕。
    也會列出「資料集區 ID」，這等同於 {{site.data.keyword.aios_short}} 實例 ID。
    {: tip}

    ![摘要檢閱](images/gs-setup-summary4.png)

1.  您的畫面可能類似於下列畫面擷取。由於您將使用 GUI 方法來為資料評分，只需選取**配置監視器**按鈕，就能完成這項設置。
    ![評分要求代碼](images/gs-config-send-scoring.png)

### 將 {{site.data.keyword.aios_short}} 連接至您的機器學習模型
{: #gs-ctmod}


1.  按一下 **Watson Machine Learning** 圖磚，然後按一下**儲存**。

1.  就本指導教學來說，請從功能表中選取您的 {{site.data.keyword.pm_full}} 實例，並按**下一步**。

    也會提供選項讓您選擇不同的 {{site.data.keyword.pm_short}} 位置。如需相關資訊，請參閱[指定 {{site.data.keyword.pm_full}} 服務實例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)。{: note}

    ![設定 {{site.data.keyword.pm_short}} 實例](images/gs-set-wml.png)

現在，您能夠選取所部署的模型，以交由 {{site.data.keyword.aios_short}} 監視。


### 為您的模型提供一組取樣資料
{: #gs-samp}

您必須先至少針對模型產生一項評分要求，以產生可供監視器取用的有效負載記載，然後您才能配置監視器。在本節中，您將以 JSON 檔案形式提供樣本資料給 Watson Studio，來產生一項評分要求。


1.  下載 [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 檔。

1.  從 Watson Studio 專案的**部署**標籤中，按一下 **credit-risk-deploy** 鏈結，按一下**測試**標籤，並選取 JSON 輸入圖示。

    ![JSON 測試](images/json_test02.png)

1.  現在，開啟您所下載的 `credit_payload_data.json` 檔，將內容複製到**測試**標籤中的 JSON 欄位。按一下**預測**按鈕，為訓練有效負載評分並傳送給您的模型。

    ![JSON 預測](images/json_test03.png)

## 後續步驟
{: #gs-next-steps-config}

完成下列步驟，以繼續進行本指導教學：

1. [準備監視器以進行部署](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy)。

   如果要準備監視器，您必須選取其中一個所部署的模型，並將它新增至儀表板。從**洞察**標籤中，按一下部署圖磚，或是按一下**新增至儀表板**按鈕，以選取所部署的模型，並按一下**配置**。

2. [設置有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data)。

   在**有效負載記載**區段中，您必須指定輸入的類型。

3. [設置模型明細](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets)。

   在**M模型明細**區段中，您必須記錄模型明細。對於本指導教學，請選取**手動配置監視器**。

4. [配置品質監視](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。

   在**品質**區段中，設定品質警示臨界值和樣本大小。

5. [配置公平性監視](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

   在**公平性**區段中，選擇要監視哪些特性的公平性。對於您選取的每一項特性，{{site.data.keyword.aios_short}} 會監視所部署模型的有利輸出結果，是否較傾向於某一個群組，而高過另一個群組。雖然特性是個別監視，但除去偏誤程序會一併更正所有特性的問題。

6. [配置漂移偵測監視器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。

   在**漂移**區段中，設置漂移偵測模型。
   
5. [提供一組樣本回饋資料給您的模型](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv)。

   為了能夠監視品質，必須提供回饋資料給您的模型。必須完成此動作，品質資料才會出現在儀表板中。您可以一併產生要求，作法是將樣本回饋資料新增至模型來進行評分。對於此作業，您將下載含有樣本回饋資料的 CSV 檔案。

6. [取得洞察](/docs/services/ai-openscale?topic=ai-openscale-io-ov)。

   在您配置精確度監視之後，會在一個小時之後執行精確度檢查。在正式作業系統中，這樣做是合理的，如此您的儀表板就能累積回饋資料。基於本指導教學的目的，您可能希望在新增回饋資料之後手動執行精確度檢查，以便可在**洞察**儀表板中看到結果。

   如果要立即檢查結果，請從**洞察**頁面中選取一項部署，按一下其中一個**品質**度量，然後按一下**立即檢查品質**。
