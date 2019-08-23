---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Python SDK 指導教學（進階）
{: #crt-ov}

在本指導教學中，您將學習執行下列作業：

- 執行 Python 記事本，以建立、訓練及部署機器學習模型。
- 建立資料集區，配置效能、精確度和公平性監視器，以及建立要監視的資料。
- 在 {{site.data.keyword.aios_short}} Insights 標籤中檢視結果。


## Python 用戶端
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 用戶端](http://ai-openscale-python-client.mybluemix.net/){: external} 是一個 Python 程式庫，可讓您直接在 {{site.data.keyword.cloud_notm}} 上使用 {{site.data.keyword.aios_short}} 服務。您可以使用 Python 用戶端而非 {{site.data.keyword.aios_short}} 用戶端使用者介面，以直接配置記載資料庫、連結您的機器學習引擎，以及選取及監視部署。如需以此方式使用 Python 用戶端的相關範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks){: external}。

## 實務
{: #crt-scenario}

傳統的貸方是在壓力之下，將其金融服務數位投資組合推廣給更大更多元的對象，這需採用新作法來為信用風險建模。他們的資料科學團隊目前仰賴標準建模技術，例如：決策樹狀結構和邏輯迴歸（這對中型資料集來說還能應付得宜），且能做出易於解釋的建議。這符合信用貸款決策必須透明且可解釋的法規需求。

為了能信用存取更廣且風險更高的族群，必須跳脫傳統信用（例如：抵押貸款和汽車貸款），來擴增申請者的信用歷程，以交替使用公用事業和行動電話方案付款歷程，外加教育和工作職稱。這些新的資料來源雖提供承諾，但也帶來風險，亦即，出現非預期相關性的可能性增加，會因為申請者的年齡、性別或其他個人特質而造成偏誤。

大多適用於這些多樣化資料集的資料科學技術（例如：梯度提升樹狀結構和神經網路）可以產生更加精確的風險模型，只是要付出代價。這類「黑盒」模型會產生不透明的預測，而必須設法變成透明，以確保能通過法規核准，例如：「一般資料保護規章 (GDPR)」第 22 條文，或「消費者金融保護局」所管理的聯邦「公平信用報告法案 (FCRA)」。

本指導教學提供的信用風險模型使用一個訓練資料集，其中含有每一個貸款申請者的 20 個相關屬性。其中兩個屬性（年齡和性別）可用來測試偏誤。在本指導教學中，焦點會放在對於性別與年齡的偏誤。如需訓練資料的相關資訊，請參閱[為何 {{site.data.keyword.aios_short}} 需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}} 會監視所部署模型的有利輸出結果（「無風險」），是否較傾向於某一個群組（參照群組），且高過另一個群組（受監視群組）。在本指導教學中，性別的「受監視群組」是 `female`，而年齡的「受監視群組」是 `18 to 25`。

## 必要條件
{: #crt-prereqs}

本指導教學利用 "Python 3.5 with Spark" 執行時期環境，來使用應在 Watson Studio 專案中執行的 Jupyter 記事本。它需要具備下列 {{site.data.keyword.cloud_notm}} 服務的服務認證：

- Cloud Object Storage（用來儲存您的 {{site.data.keyword.DSX}} 專案）
- {{site.data.keyword.aios_short}}
- {{site.data.keyword.pm_full}}
- （選用）Databases for PostgreSQL 或 Db2 Warehouse

Jupyter 記事本會訓練、建立和部署一個 German Credit Risk 模型，配置 {{site.data.keyword.aios_short}} 以監視該部署，以及提供 7 天的歷程記錄和測量，以供在 {{site.data.keyword.aios_short}} Insights 儀表板中檢視。您也可以選擇性地配置模型，以便使用 Watson Studio 和 Spark 來持續學習。

## 簡介
{: #crt-intro}

在本指導教學中，您將執行下列作業：

- [佈建 {{site.data.keyword.cloud_notm}} 機器學習和儲存服務](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-services)。
- [設置一個 Watson Studio 專案，並執行 Python 記事本，以建立、訓練及部署機器學習模型](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-set-wstudio)。
- [佈建 {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-wos-adv)。
- [執行 Python 記事本，以建立資料集區，配置效能、精確度和公平性監視器，以及建立資料來監視](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-edit-notebook)。
- [在 {{site.data.keyword.aios_short}} 的「洞察」標籤中檢視結果](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-view-results)。

## 佈建 {{site.data.keyword.cloud_notm}} 服務
{: #crt-services}

使用您的 {{site.data.keyword.ibmid}}，登入 [{{site.data.keyword.cloud_notm}} 帳戶](https://{DomainName}){: external}。在佈建服務時（尤其如果您使用 Db2 Warehouse），請驗證對於所有服務，您選取的組織和空間都是相同的。

### 建立 {{site.data.keyword.DSX}} 帳戶
{: #crt-wstudio}

- 如果您的帳戶尚無相關聯的實例，請[建立一個 {{site.data.keyword.DSX}} 實例](https://{DomainName}/catalog/services/watson-studio){: external}：

  ![顯示 Watson Studio 圖磚](images/watson_studio.png)

- 為您的服務命名，選擇 Lite（免費）方案，並按一下**建立**按鈕。

### 佈建 {{site.data.keyword.cos_full_notm}} 服務
{: #crt-cos}

- 如果您的帳戶尚無相關聯的服務，[請佈建一項 {{site.data.keyword.cos_short}} 服務](https://{DomainName}/catalog/services/cloud-object-storage){: external}。

  ![顯示 Object Storage 圖磚](images/object_storage.png)

- 為您的服務命名，選擇 Lite（免費）方案，並按一下**建立**按鈕。

### 佈建 {{site.data.keyword.pm_full}} 服務
{: #crt-wml}

- 如果您的帳戶尚無相關聯的實例，請[佈建一個 {{site.data.keyword.pm_short}} 實例](https://{DomainName}/catalog/services/machine-learning){: external}：

  ![顯示 Machine Learning 圖磚](images/machine_learning.png)

- 為您的服務命名，選擇 Lite（免費）方案，並按一下**建立**按鈕。

### 佈建 {{site.data.keyword.aios_full}} 服務
{: #crt-wos-adv}

如果您尚未這樣做，請確定您已佈建 {{site.data.keyword.aios_full}}。 

- 如果您的帳戶尚無相關聯的實例，請[佈建一個 {{site.data.keyword.aios_short}} 實例](https://{DomainName}/catalog/services/watson-openscale){: external}：

  顯示 ![{{site.data.keyword.aios_short}} 圖磚](images/wos-cloud-tile.png)

1. 按一下**型錄** > **AI** > **{{site.data.keyword.aios_short}}**。
2. 為您的服務命名，選擇一種方案，並按一下**建立**按鈕。
3. 若要啟動 {{site.data.keyword.aios_short}}，請按一下**入門**按鈕。

### （選用）佈建 Databases for PostgreSQL 或 Db2 Warehouse 服務
{: #crt-db2}

如果您已有一個付費 {{site.data.keyword.cloud_notm}} 帳戶，您可以佈建 `Databases for PostgreSQL` 或 `Db2 Warehouse` 服務，以便充分利用與 {{site.data.keyword.DSX}} 的整合及持續學習服務。如果您選擇不佈建付費服務，您可以將免費的內部 PostgreSQL 儲存空間與 {{site.data.keyword.aios_short}} 搭配使用，只是這就無法為模型配置持續學習。

- [佈建 Databases for PostgreSQL 服務](https://{DomainName}/catalog/services/databases-for-postgresql){: external}或 [Db2 Warehouse 服務](https://{DomainName}/catalog/services/db2-warehouse){: external}（如果您的帳戶尚無此服務的話）：

  ![顯示 DB for Postgres 圖磚](images/dbpostgres.png)

  ![顯示 Db2 Warehouse 圖磚](images/db2_warehouse.png)

- 為您的服務命名，選擇「標準」方案 (Databases for PostgreSQL) 或「入門」方案 (Db2 Warehouse)，並按一下**建立**按鈕。

## 設置 {{site.data.keyword.DSX}} 專案
{: #crt-set-wstudio}

- 登入 [{{site.data.keyword.DSX}} 帳戶](https://dataplatform.ibm.com/){: external}。按一下 {{site.data.keyword.avatar}}，並驗證您使用的帳戶就是您用來建立 {{site.data.keyword.cloud_notm}} 服務的相同帳戶：

  ![相同帳戶](images/same_account.png)

- 在 {{site.data.keyword.DSX}}中，以建立新專案做為開始。選取「建立專案」：

  ![Watson Studio - 建立專案](images/studio_create_proj.png)

- 選取**標準**圖磚，以建立專案：

  ![顯示「Watson Studio - 選取標準專案」圖磚](images/studio_create_standard.png)

- 為專案提供名稱和說明，在**儲存空間**下拉功能表中，確定已選取您建立的 Cloud Object Storage 服務，並按一下**建立**。


## 建立和部署 {{site.data.keyword.pm_short}} 模型
{: #crt-make-model}

### 將 `Working with Watson Machine Learning` 記事本新增至 {{site.data.keyword.DSX}} 專案
{: #crt-add-notebook}

- 存取下列檔案。如果您具有 GitHub 帳戶，可以登入以複製及下載檔案。否則，您可以按一下**原始**按鈕，以檢視原始版本，並將檔案文字複製到新檔案，且其副檔名為 .ipynb。

    - [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}

- 從 {{site.data.keyword.DSX}} 專案的**資產**標籤中，按一下**新增至專案**按鈕，並從下拉功能表中選取**記事本**：

  ![顯示「選擇資產類型」，其中強調顯示了記事本圖磚](images/add_notebook.png)

- 選取**從檔案**：

  ![新建記事本表單](images/new_notebook_name.png)

- 然後按一下**選擇檔案**按鈕，選取您所下載的 "german_credit_lab.ipynb" 記事本檔案：

  ![新建記事本表單](images/new_notebook_name2a.png)

- 在**選取執行時期**區段中，選擇最新的 Python 3.5 with Spark 選項：

- 按一下**建立記事本**。

### 編輯及執行 `Working with Watson Machine Learning` 記事本
{: #crt-edit-notebook}

`Working with Watson Machine Learning` 記事本含有您將執行之 Python 程式碼中每一個步驟的詳細指示。當您在完成記事本期間，請花一些時間瞭解每一個指令的作用。
{: tip}

- 從 Watson Studio 專案的**資產**標籤中，按一下 `Working with Watson Machine Learning` 記事本旁的**編輯**圖示，以編輯它。

- 在「佈建服務及配置認證」區段中，進行下列變更：

    - 遵循記事本中的指示，來建立、複製和貼上 {{site.data.keyword.cloud_notm}} API 金鑰。

    - 將 {{site.data.keyword.pm_full}} 服務認證取代為您先前建立的認證。

    - 將資料庫認證取代為您建立給 Databases for PostgreSQL 的認證。

    - 如果您先前已將 {{site.data.keyword.aios_short}} 配置成使用免費的內部 PostgreSQL 資料庫來作為資料集區，您可以切換至使用 Databases for PostgreSQL 服務的新資料集區。如果要刪除舊有 PostgreSQL 配置，並建立新配置，請將 KEEP_MY_INTERNAL_POSTGRES 變數設為 `False`。

        記事本會移除您現有的內部 PostgreSQL 資料集區，並以所提供的資料庫認證，來建立新的資料集區。**不會進行任何的資料移轉**。{: important}

- 在您佈建服務並輸入認證之後，您的記事本就準備好可執行。按一下**核心**功能表項目，並從功能表中選取**重新啟動並清除輸出**：


  ![重新啟動並清除](images/restart_and_clear.png)

- 現在，依序執行記事本的每一個步驟。請如所述，注意每一個步驟所發生的情況。請完成所有步驟，直到並包括「有助於除錯的其他資料」一節中的步驟。

最終結果會是您已建立、訓練及部署 **Spark German Risk Deployment** 模型至您的 {{site.data.keyword.aios_short}} 服務實例。{{site.data.keyword.aios_short}} 會配置成檢查模型對於性別（在本例中是「女性」）或年齡（在本例中是「18 歲到 25 歲」）是否有偏誤。

## 檢視結果
{: #crt-view-results}

### 檢視您部署的相關洞察
{: #crt-view-insights}

使用 [{{site.data.keyword.aios_short}} 儀表板](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}，按一下**洞察**標籤：


  ![顯示「洞察」圖示](images/insight-dash-tab.png)

「洞察」頁面提供已部署模型的度量概觀。如果「公平性」或「精確度」度量超出執行記事本時所設定的臨界值，您很容易就可以看到相關警示。本指導教學中使用的資料和設定會建立與這裡所示類似的「精確度」和「公平性」度量。

  ![顯示「洞察概觀」儀表板，其中有一個 German Credit Risk 模型的圖磚](images/insight-overview-adv-tutorial-2.png)

### 檢視您部署的監視資料
{: #crt-view-mon-data}

1. 如果要檢視監視明細，請從**洞察**頁面，按一下對應至該部署的圖磚。會出現該項部署的監視資料。 
2. 在圖表中滑動標記，以選取某特定一小時時間範圍的資料。 
3. 按一下**檢視明細**鏈結。

  ![監視資料](images/insight-monitor-data2.png)

現在，您可以檢閱您所監視之資料的圖表。就本例而言，您可以看到在「性別」特性方面，`female` 群組收到的「無風險」有利輸出結果 (68%) 小於 `male` 群組 (78%)。
  ![「洞察」概觀](images/insight-review-charts2.png)

### 檢視模型交易的可解釋性
{: #crt-view-explain}

對於每一項部署，您可以查看特定交易的可解釋性資料。

如果您已知道您想檢視哪一項交易，快速的作法是使用交易 ID 來查閱它。在您按一下部署圖磚之後，請從導覽器按一下**解釋交易** ![「解釋交易」標籤](images/insight-transact-tab.png) 圖示，輸入交易 ID，並按 **Enter** 鍵。
{: tip}

如果您使用 PostgreSQL 內部精簡版本，您可能無法擷取您的資料庫認證。這可能使您無法查看交易。
{: note}

1. 從最新偏誤資料的圖表中，按一下**檢視交易**按鈕。

  ![檢視交易](images/view_transactions.png)

  會出現以偏誤方式執行部署的交易清單。 
  
2. 選取其中一項交易，並從**動作**直欄中，按一下**解釋**鏈結。

  ![交易清單](images/transaction_list_cr.png)

現在，您會看到模型是如何得出其結論的相關解釋，包括：模型的信賴度、確信層次的造成因素，以及輸送給模型的屬性。

  ![檢視交易](images/view_transaction_cr.png)
  
## 後續步驟
{: #crt-next-steps}

- 進一步瞭解[檢視及解讀資料](/docs/services/ai-openscale?topic=ai-openscale-it-ov)和[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。
