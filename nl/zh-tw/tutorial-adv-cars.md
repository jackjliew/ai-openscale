---

title: 利用 {{site.data.keyword.aios_short}} 讓您的機器學習模型可信任且具透明度
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 指導教學（進階）
{: #tadv-tutorial-advanced}

## 實務
{: #tadv-scenario}

租車公司已收集關於客戶滿意度的回饋資料。所提供的模型會使用此資料，來預測後續要對客戶採取的行動方針，例如，在他們下次租賃時提供一個憑單。

模型使用客戶資料欄位 ID（ID 號碼）、性別、狀態（單身或已婚）、小孩（人數）、年齡、客戶狀態（作用中或非作用中）、車主（是或否）、客戶服務（客戶註解）、滿意度（滿意或不滿意），以及業務領域（與產品或服務相關），來預測「動作」資料欄位的四個值中的一個（NA、憑單、免費升級、隨需挑選）。

## 必要條件
{: #tadv-prereqs}

如果要完成本指導教學，您需要：

- [Watson Studio ![External link icon](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://dataplatform.ibm.com/){: new_window} 帳戶。
- [{{site.data.keyword.cloud_notm}} ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}){: new_window} 帳戶。

在本指導教學期間，您將佈建下列「精簡（免費）」{{site.data.keyword.cloud_notm}} 服務：

- Machine Learning
- Apache Spark
- Object Storage

您也將佈建下列**付費** {{site.data.keyword.cloud_notm}} 服務：

- PostgreSQL

  只要使用信用卡轉換成付費帳戶，即可取得 $200 {{site.data.keyword.cloud_notm}} 信用額度。如果您已有付費帳戶，會有一個月針對您所支付的第一個 GB 儲存空間費用，一次性退款 $16 給您。{: tip}

PostgreSQL 資料庫和 Watson Machine Learning 實例必須部署在相同的 {{site.data.keyword.cloud_notm}} 帳戶中。
{: important}

如果您已佈建必要的服務（例如，如果您已完成其他指導教學），請繼續執行下述的[設置 Watson Studio 專案](#tadv-setup-ws)。

## 簡介
{: #tadv-intro}

在本指導教學中，您將：

- 佈建 {{site.data.keyword.cloud_notm}} 機器學習和儲存服務
- 設置一個 Watson Studio 專案，並執行 Python 記事本，以建立、訓練及部署機器學習模型
- 執行 Python 記事本，以建立資料集區，配置效能、精確度和公平性監視器，以及建立資料來監視
- 在 {{site.data.keyword.aios_short}} Insights 標籤中檢視結果

## 佈建 {{site.data.keyword.cloud_notm}} 服務
{: #tadv-svcs}

以您的 IBM ID 登入 [{{site.data.keyword.cloud_notm}} 帳戶 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}){: new_window}。在佈建服務時（尤其是 Apache Spark、Object Storage 和 Db2 Warehouse 方面），請驗證對於所有服務，您選取的組織和空間都是相同的。

### 建立 Watson Studio 帳戶
{: #tadv-stac}

- 如果您的帳戶尚無相關聯的 Watson Studio 實例，請[建立 Watson Studio 實例 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/watson-studio){: new_window}：

  ![Watson Studio](images/watson_studio.png)

- 為您的服務命名，選擇「精簡（免費）」方案，並按一下**建立**按鈕。

### 佈建 Machine Learning 服務
{: #tadv-pml}

- 如果您的帳戶尚無相關聯的 Watson Machine Learning 實例，請[佈建 Watson Machine Learning 實例 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/machine-learning){: new_window}：

  ![Machine Learning](images/machine_learning.png)

- 為您的服務命名，選擇「精簡（免費）」方案，並按一下**建立**按鈕。

- 記下 Machine Learning 服務認證。在您的機器學習實例中，按一下頁面左側的**服務認證**鏈結。為認證命名，並按一下**新增**。然後從認證清單中，按一下**檢視認證**，並且複製認證，以供之後使用。

### 佈建 Spark 服務
{: #tadv-ps}

- 如果您的帳戶尚無相關聯的 Spark 服務，請[佈建 Spark 服務 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/apache-spark){: new_window}：

  ![Apache Spark](images/spark.png)

- 指派名稱給您的服務，選擇「精簡（免費）」方案，並按一下**建立**按鈕。

- 記下您 Spark 實例的服務認證。開啟 Spark 實例，並按一下左側功能表中的**服務認證**。按一下**新建認證**按鈕，為您的認證命名，並按一下**新增**。然後，按一下您剛建立之集合旁的**檢視認證**鏈結，並複製這些認證，以供之後使用。

### 佈建 Object Storage 服務
{: #tadv-pos}

- 如果您的帳戶尚無相關聯的 Object Storage 服務，請[佈建 Object Storage 服務 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}：

  ![Object Storage](images/object_storage.png)

- 為您的服務命名，選擇「精簡（免費）」方案，並按一下**建立**按鈕。

### 佈建付費 PostgreSQL 服務
{: #tadv-ppgs}

- 如果您的帳戶尚無相關聯的付費 PostgreSQL 服務，請[佈建付費 PostgreSQL 服務 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window}。

  ![Compose for PostgreSQL](images/postgres.png)

- 為您的服務命名，選擇「標準」方案，並按一下**建立**按鈕。

  只要使用信用卡轉換成付費帳戶，即可取得 $200 {{site.data.keyword.cloud_notm}} 信用額度。如果您已有付費帳戶，會有一個月針對您所支付的第一個 GB 儲存空間費用，一次性退款 $16 給您。{: tip}

- 記下您 PostgreSQL 實例的服務認證。開啟您現有（或新建）的 PostgreSQL 實例，並按一下左側功能表中的**服務認證**。按一下**新建認證**按鈕，為您的認證命名，並按一下**新增**。然後，按一下您剛建立之集合旁的**檢視認證**鏈結，並複製這些認證，以供之後使用。

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![手動設定資料類型](images/data-type-manual.png)

- 現在，訓練資料現在應會正確顯示在直欄中。按「下一步」以繼續，然後按一下「開始載入」來載入資料。--->

## 設置 Watson Studio 專案
{: #tadv-setup-ws}

- 登入您的 [Watson Studio 帳戶 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://dataplatform.ibm.com/){: new_window}。按一下右上方的帳戶 Avatar 圖示，並驗證您使用的帳戶，就是您用來建立 {{site.data.keyword.cloud_notm}} 服務的相同帳戶：  ![相同帳戶](images/same_account.png)
- 在 Watson Studio 中，開始時，請先建立一個新專案。選取「建立專案」：

  ![Watson Studio - 建立專案](images/studio_create_proj.png)

- 選取**標準**圖磚，以建立專案：

  ![Watson Studio - 選取「標準」專案](images/studio_create_standard.png)
- 為專案提供名稱和說明，在**儲存空間**下拉功能表中，確定已選取您在先前步驟中建立的 Object Storage 服務，並按一下**建立**。

### 使您的 {{site.data.keyword.cloud_notm}} 服務與 Watson 專案產生關聯
{: #tadv-acsw}

- 開啟 Watson Studio 專案，並選取**設定**標籤。在**相關聯的服務**區段中，按一下**新增服務**下拉功能表，並選取 **Watson**：

  ![新增 Watson 服務](images/add_watson_service.png)

- 按一下**機器學習**圖磚上的**新增**鏈結，並選取**現有**標籤。從**現有服務實例**下拉功能表中，選擇您在前一區段中建立的服務，然後按一下**選取**。

- 從「專案設定」標籤中，再次選取**新增服務**，並從下拉功能表中選擇 **Spark**。從**現有**標籤中，選擇您建立的 Spark 服務，並按一下**選取**。

## 建立和部署機器學習模型
{: #tadv-deploy-ml}

### 新增 `CARS4U Action Recommendation - model` 記事本至您的 Watson Studio 專案

- 下載下列檔案：

    - [CARS4UAction Recommendation - model ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- 從您 Watson Studio 專案的**資產**標籤中，按一下**新增至專案**按鈕，並從下拉功能表中選取**記事本**：

  ![新增連線](images/add_notebook.png)

- 選取**從檔案**：

  ![新建記事本表單](images/new_notebook_name.png)

- 然後按一下**選擇檔案**按鈕，選取您所下載的 "CARS4U Action Recommendation - model"：

  ![新建記事本表單](images/new_notebook_name2.png)

- 在**選取執行時期**區段中，從下拉清單中選擇您先前建立的 Spark 實例：

  ![Spark 執行時期](images/spark_runtime.png)

- 按一下**建立記事本**。

### 編輯及執行 `CARS4U Action Recommendation - model` 記事本
{: #tadv-ern}

`CARS4U Action Recommendation - model` 記事本含有您將執行之 Python 程式碼中每一個步驟的詳細指示。當您在完成記事本期間，請花一些時間瞭解每一個指令的作用。
{: tip}

- 從 Watson Studio 專案的**資產**標籤中，按一下 `CARS4U Action Recommendation - model` 記事本旁的**編輯**圖示，以編輯它。

- 在第 2.2 節「上傳資料至 PostgreSQL 資料庫」中，將 Postgres 服務認證取代為您在前一區段所建立的認證。

- 在第 4 節「將模型儲存在儲存庫」中的**提示**之下，將 Watson Machine Learning 認證取代為您在前一區段所建立的認證。

- 輸入認證之後，您的記事本就準備好可執行。按一下**核心**功能表項目，並從功能表中選取**重新啟動並全部執行**：
  ![重新啟動並執行](images/restart_and_run.png)

這會在您的專案中建立、訓練及部署 **CARS4U - Action Recommendation Model**。您可以選取 Watson Studio 專案的**部署**標籤，並按一下 **CARS4U - Area and Action Model Deployment** 鏈結，來驗證模型已部署。
## 配置 {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### 佈建 {{site.data.keyword.aios_short}}
{: #tadv-paios}

- 如果您尚未佈建 {{site.data.keyword.aios_short}} 實例，請從您的 {{site.data.keyword.cloud_notm}} 帳戶，按一下**型錄**鏈結，並依 "OpenScale" 來過濾。選取 {{site.data.keyword.aios_short}} 的圖磚。

<!---
  ![{{site.data.keyword.aios_short}}](images/openscale.png)
--->

- 為您的服務命名，選取「精簡」方案，並按一下**建立**。
### 將 {{site.data.keyword.aios_short}} 連接至您的機器學習模型
{: #tadv-cmlm}

由於機器學習模型已部署，您可以配置 {{site.data.keyword.aios_short}}，以確保您的模型具備信任和透明。選取您 {{site.data.keyword.aios_short}} 實例的**管理**標籤，並按一下**啟動應用程式**按鈕。會開啟「開始使用 {{site.data.keyword.aios_full}}」頁面；請按一下**開始**。
- 選取 "Watson Machine Learning" 圖磚，並按**下一步**。

  ![設定 WML 實例](images/gs-wml-default.png)

- 從下拉功能表中選取 Watson Machine Learning 實例，並按**下一步**。

  ![設定 WML 實例](images/gs-set-wml.png)

- 現在，您能夠選取要將哪些所部署的模型交由 {{site.data.keyword.aios_short}} 監視。請檢查您所建立和部署的模型；按**下一步**以接受此模型：
  ![選取所部署的模型](images/gs-set-deploy.png)

- 接下來，您需要選擇 PostgreSQL 資料庫。您有兩個選項：免費「精簡」方案資料庫，或是現有或新的資料庫。對於本指導教學，請選取**使用現有資料庫或購買新資料庫**圖磚。
    ![選取資料庫](images/gs-set-lite-db1.png)

  請參閱 [指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)主題中關於每一個選項的更完整詳細資料。
  {: note}

- 一旦您選取「使用現有資料庫或購買新資料庫」選項，{{site.data.keyword.aios_short}} 會檢查您的 {{site.data.keyword.cloud_notm}} 帳戶，以找出您現有的 Compose for PostgreSQL 資料庫。
  從**綱目**下拉功能表中，選取 "data_mart" 綱目。

  ![選取資料庫](images/gs-set-schema1.png)

- 選取資料庫和綱目之後，請按**下一步**，檢閱摘要資料，並按一下**儲存**。
  ![選取資料庫](images/gs-setup-summary3.png)

  當出現提示時，請按一下**結束儀表板**。

## 建立資料集區，並配置效能、精確度和公平性監視器
{: #tadv-config-monitors}

### 將 `{{site.data.keyword.aios_short}} and Watson ML engine` 記事本新增至 Watson Studio 專案
{: #tadv-aomn}

`{{site.data.keyword.aios_short}} and Watson ML engine` 記事本含有您將執行之 Python 程式碼中每一個步驟的詳細指示。當您在完成記事本期間，請花一些時間瞭解每一個指令的作用。
{: tip}

- 下載下列檔案：

    - [{{site.data.keyword.aios_short}}and Watson ML engine ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- 從您 Watson Studio 專案的**資產**標籤中，按一下**新增至專案**按鈕，並從下拉功能表中選取**記事本**：
  ![新增連線](images/add_notebook.png)

- 選取**從檔案**：

  ![新建記事本表單](images/new_notebook_name.png)

- 然後按一下**選擇檔案**按鈕，選取您所下載的 "{{site.data.keyword.aios_short}} and Watson ML engine"：
  ![新建記事本表單](images/new_notebook_name3.png)

- 在**選取執行時期**區段中，從下拉清單中選擇您先前建立的 Spark 實例：

  ![Spark 執行時期](images/spark_runtime.png)

- 按一下**建立記事本**。

### 編輯及執行 `{{site.data.keyword.aios_short}} and Watson ML engine` 記事本
{: #tadv-eromn}

- 從 Watson Studio 專案的**資產**標籤中，按一下 `{{site.data.keyword.aios_short}} and Watson ML engine` 記事本旁的**編輯**圖示，以編輯它。

- 在第 1.1 節「安裝和鑑別」中：

    - 在**動作：取得 instance_id (GUID) 和 API 金鑰**之下，遵循指示以取得認證。將 `aios_credentials` 取代為您自己的認證。
    - 接著，在**動作：在這裡新增 Watson Machine Learning 認證**中，將 Watson Machine Learning 認證取代為您先前建立的認證。

    - 最後，在**動作：在這裡新增 PostgreSQL 認證**中，將 PostgreSQL 認證取代為您先前建立的認證。

- 輸入認證之後，您的記事本就準備好可執行。按一下**核心**功能表項目，並從功能表中選取**重新啟動並全部執行**：
  ![重新啟動並執行](images/restart_and_run.png)

  這會設置資料集區，啟用承載內容記載，配置效能、精確度和公平性監視器並加以評分，以及將那些度量提供給您的 {{site.data.keyword.aios_short}} 實例。
## 檢視結果
{: #tadv-results}

### 檢視您部署的相關洞察
{: #tadv-vide}

使用 [{{site.data.keyword.aios_short}} 儀表板 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}，按一下**洞察**標籤：
  ![洞察](images/insight-dash-tab.png)

「洞察」頁面提供已部署模型的度量概觀。您很容易就可看到「公平性」或「精確度」度量的相關警示，這些度量已低於執行記事本時所設定的臨界值 (70%)。本指導教學中使用的資料和設定會建立與這裡所示類似的「精確度」和「公平性」度量。

  ![「洞察」概觀](images/insight-overview-adv-tutorial.png)

### 檢視您部署的監視資料
{: #tadv-vmdd}

按一下「洞察」頁面上的圖磚，以選取部署。會出現該項部署的監視資料。在圖表中滑動標記，以選取您執行記事本那段時間範圍的資料。然後選取**檢視明細**鏈結。
  ![監視資料](images/insight-monitor-data1.png)

現在，您可以檢閱您所監視之資料的圖表。就本例而言，您可以使用**特性**下拉功能表，來選取「小孩」或「性別」，以查看受監視資料的相關明細。  ![「洞察」概觀](images/insight-review-charts1.png)

<!---

### 檢視模型交易的可解釋性
{: #tadv-vemt}

針對您所監視的資料，從圖表中選取「檢視交易」按鈕。
  ![檢視交易](images/view_transactions.png)

  會列出過去一小時的交易清單。複製其中一個交易 ID。

  ![交易清單](images/transaction_list.png)

使用 [{{site.data.keyword.aios_short}} 儀表板 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}，按一下「可解釋性」標籤：

  ![可解釋性](images/explainability.png)

貼上您複製到搜尋方框的交易 ID 值，並按下鍵盤上的 **Return** 鍵。現在，您會看到模型是如何得出其結論的相關解釋，包括：模型的確信程度、確信層次的造成因素，以及輸送給模型的屬性。

  ![檢視交易](images/view_transaction1.png)

--->

## 後續步驟
{: #tadv-next}

- 進一步瞭解[檢視及解讀資料](/docs/services/ai-openscale?topic=ai-openscale-it-ov)和[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。
