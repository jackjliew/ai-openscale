---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

在本指導教學中，您將執行下列步驟：

- [佈建 {{site.data.keyword.Bluemix_notm}} 機器學習和儲存服務](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps)。
- [設置一個 Watson Studio 專案，並建立、訓練及部署機器學習模型](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup)。
- [配置及探索您模型的信任、透明度和可解釋性](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios)。

## 佈建 {{site.data.keyword.Bluemix_notm}} 必備服務
{: #gs-prps}

除了 {{site.data.keyword.aios_short}}，如果要完成本指導教學，您需要具備下列帳戶和服務。

**重要事項**：為求最佳效能，建議將必備服務建立在與 {{site.data.keyword.aios_short}} 相同的地區中。如果要檢視 {{site.data.keyword.aios_short}} 的可用位置，請參閱[服務可用性](/docs/resources?topic=resources-services_region)。

1.  使用您的 {{site.data.keyword.ibmid}}，登入 [{{site.data.keyword.Bluemix_notm}} 帳戶](https://{DomainName}){: external}。
1.  對於尚未與您帳戶相關聯的下列每一項服務，請按一下此鏈結，為服務命名，選取 **Lite**（免費）方案，並按一下**建立**按鈕，來建立一個實例：

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## 設置 Watson Studio 專案
{: #gs-setup}

1.  登入 [Watson Studio 帳戶](https://dataplatform.ibm.com/){: external}，並從建立新專案開始。選取**新建專案**。

    ![Watson Studio - 建立專案](images/studio_create_proj.png)

1.  選取**標準**圖磚。

    ![Watson Studio - 選取「標準」專案](images/studio_create_standard.png)

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


    ![新建記事本表單](images/credit-sample-model.png)

### 部署 `Credit Risk` 模型
{: #gs-depmod}

1.  從 `Credit Risk` 模型頁面，按一下**部署**標籤，然後按一下**新增部署**。
1.  輸入 `credit-risk-deploy` 作為部署名稱，並選取 **Web 服務**部署類型。
1.  按一下**儲存**。

## 配置 {{site.data.keyword.aios_short}}
{: #gs-confaios}

### 佈建 {{site.data.keyword.aios_short}}
{: hide-dashboard}
{: #gs-provaios}

1.  [佈建新的 {{site.data.keyword.aios_short}} 服務實例](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/openscale.png)

2.  為您的服務命名，選取 **Lite 方案**，並按一下**建立**。

### 將 {{site.data.keyword.aios_short}} 連接至您的機器學習模型
{: #gs-ctmod}

到目前為止，機器學習模型已部署，您可以配置 {{site.data.keyword.aios_short}}，以確保您的模型具備可信任性與透明度。


1.  選取您 {{site.data.keyword.aios_short}} 實例的**管理**標籤，並按一下**啟動應用程式**按鈕。會開啟**歡迎使用 {{site.data.keyword.aios_short}}** 示範頁面。
2. 對於本指導教學，請按一下**否，謝謝**，然後按一下**開始**。

1.  按一下 **Watson Machine Learning** 圖磚。

1.  就本指導教學來說，請從功能表中選取您的 {{site.data.keyword.pm_full}} 實例，並按**下一步**。

    也會提供選項讓您選擇不同的 {{site.data.keyword.pm_short}} 位置。如需相關資訊，請參閱[指定 {{site.data.keyword.pm_full}} 服務實例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)。{: note}

    ![設定 {{site.data.keyword.pm_short}} 實例](images/gs-set-wml.png)

1.  現在，您能夠選取所部署的模型，以交由 {{site.data.keyword.aios_short}} 監視。選取您所建立和部署的模型，並按**下一步**。

    ![選取所部署的模型](images/gs-set-deploy0.png)

1.  接下來，您需要選擇資料庫。您有兩個選項：免費資料庫，或是現有資料庫或新的資料庫。對於本指導教學，請選取**使用 {{site.data.keyword.aios_short}} 代管的免費資料庫**磚。

    免費資料庫有一些重要限制。它是一個代管資料庫，並未給予您個別存取權。它讓 {{site.data.keyword.aios_short}} 能夠存取您的資料庫和資料。它不符合 GDPR 標準。有關每一個選項的更多完整詳細資料，請參閱[指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)主題。現有的資料庫可以是 PostgreSQL 資料庫或 Db2 資料庫。{: tip}

    ![選取資料庫](images/gs-set-lite-db2.png)

1.  檢閱摘要資料，並按一下**儲存**。當確認並出現提示時，請按一下**繼續配置**按鈕。
    也會列出「資料集區 ID」，這等同於 {{site.data.keyword.aios_short}} 實例 ID。
    {: tip}

    ![摘要檢閱](images/gs-setup-summary4.png)

1.  您的畫面可能類似於下列畫面擷取。由於您將使用 GUI 方法來為資料評分，只需選取**配置監視器**按鈕，就能完成這項設置。
    ![評分要求代碼](images/gs-config-send-scoring.png)

### 為您的模型提供一組取樣資料
{: #gs-samp}

您必須先至少針對模型產生一項評分要求，以產生可供監視器取用的有效負載記載，然後您才能配置監視器。在本節中，您將以 JSON 檔案形式提供樣本資料，來產生一項評分要求。

1.  下載 [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 檔。

1.  從 Watson Studio 專案的**部署**標籤中，按一下 **credit-risk-deploy** 鏈結，按一下**測試**標籤，並選取 JSON 輸入圖示。

    ![JSON 測試](images/json_test02.png)

1.  現在，開啟您所下載的 `credit_payload_data.json` 檔，將內容複製到**測試**標籤中的 JSON 欄位。按一下**預測**按鈕，為訓練有效負載評分並傳送給您的模型。

    ![JSON 預測](images/json_test03.png)

### 準備監視
{: #gs-prepmon}

1.  現在，在 {{site.data.keyword.aios_short}} 實例中，選取您的部署，並按一下**開始**。

    ![選取部署](images/config-select-deploy2.png)

1.  指定內含模型預測之回答的特性。（在您的資料庫中，表格中的哪一個直欄包含預測值或標籤？）在此案例中，模型將預測信用風險，因此請選取**風險**直欄，並按**下一步**。

    ![準備監視](images/config-prep-monitor.png)

1.  接下來，您將提供模型及訓練資料的相關資訊。按**下一步**。

    ![準備解釋](images/config-what-monitor.png)

1.  從**資料類型**功能表中，選取**數值/種類**作為您部署分析的資料類型，然後按**下一步**。

    ![選取輸入類型](images/config-input-monitor.png)

1.  對於數值或種類資料，您需要提供模型訓練資料的相關資訊，才能配置監視器。請選取**手動配置監視器**，以提供您訓練資料的連線資訊。

    ![選取配置類型](images/config-manual-monitor.png)

1.  在監視模型度量時，演算法類型很重要，例如「精確度」。由於模型可以做出的預測是「風險」或「無風險」，請選取**二進位分類**[演算法類型](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)，並按**下一步**。

    ![二進位](images/binary.png)

1.  在下列畫面中，會預先移入樣本資料的位置資訊。請選取**下一步**繼續。

    ![「指定訓練資料的 Db2 位置」頁面](images/gs-config-train-db2-monitor.png)

1.  此外，也會預先移入綱目和表格。按**下一步**以繼續。

    ![指定綱目和訓練表格中的 Db2 位置](images/gs-fair-config-table-db2.png)

1.  現在，您必須指定含有模型所要預測之回答的特性（亦即，在您的資料庫中，表格中的哪一個直欄含有預測值（標籤））。在本例中，模型將預測信用風險，因此請選取**風險**直欄，並按**下一步**。

    您的訓練資料庫具有一些您為了訓練模型而提供的值。{: note}

    ![預測標籤的輸入](images/gs-config-label.png)

1.  選取用來訓練模型的直欄。這是您模型部署在要求中所預期的資料。`_training` 以外的所有資料直欄，都是模型的輸入。請選取其他所有輸入，並按**下一步**。

    ![可解釋性輸入](images/explain_inputs1.png)

1.  對於種類資料，您必須識別現在雖含有整數但原本卻是含有文字值的那些直欄。請依這裡所示來選取值。

    ![可解釋性輸入](images/config_categories.png)

1.  檢閱您的選擇摘要，按一下**儲存**，然後按一下**確定**。

### 配置「公平性」監視
{: #gs-cfgfair}

1.  按一下**公平性**。

1.  閱讀有關公平性的說明，並按**下一步**。如需相關資訊，請參閱[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

1.  現在您可以針對公平性，選擇所要監視的特性。對於您選取的每一項特性，{{site.data.keyword.aios_short}} 會監視所部署模型的有利輸出結果，是否較傾向於某一個群組，而高過另一個群組。在本例中，我們將監視**性別**和**年齡**特性。

    這些特性採個別監視，但是任何的除去偏誤都會一併更正所有特性的問題。請按一下**性別**和**年齡**圖磚，並按**下一步**。

1.  {{site.data.keyword.aios_short}} 會運作，藉由比較參照群組，來偵測對於受監視群組的偏誤。對於**性別**特性，請將值 `male` 新增至**參照群組**，將值 `female` 新增至**受監視群組**，並按**下一步**。

    對於**性別**，如果受監視群組的「風險」預測比例，不同於參照群組的比例，則會將模型標示為「有偏誤」。因此，如果模型預測男性客戶當時的「風險」是 60%，女性客戶當時的「風險」是 20%，表示有偏誤。

    ![性別群組](images/gender_groups1.png)

1.  指派公平性臨界值給**性別**。如果公平性評比超出您設定的臨界值，作業儀表板會顯示警示。請將臨界值設為 90%，並按**下一步**。

1.  對於**年齡**特性，請將值 `26-74` 新增至**參照群組**，將值 `19-25` 新增至**受監視群組**，並按**下一步**。

    如同**性別**，在**年齡**方面，如果受監視群組的「風險」預測比例，不同於參照群組的比例，則會將模型標示為「有偏誤」。因此，如果 26 歲到 74 歲客戶所收到的「風險」預測比例，不同於 19 歲到 25 歲客戶的比例，表示模型有偏誤。

    ![BP 群組](images/age_groups.png)

1.  請針對**年齡**，將臨界值設為 90%，並按**下一步**。

1.  將**來自訓練資料的值**欄位中的值，拖放至**有利值**和**不利值**欄位。對於本指導教學，有利值是**無風險**，不利值是**風險**。按**下一步**。

    {{site.data.keyword.aios_short}} 會自動偵測有效負載記載中哪些直欄含有預測值，並將它們呈現在**來自訓練資料的值**欄位中。請注意，儘管您的訓練資料庫具有您提供用來訓練模型的值，有效負載記載資料庫會包含在模型執行時期所收集的回饋資料，可讓您之後選擇性地用來重新訓練和重新部署您的模型。{: note}

    ![正值和負值](images/pos_and_neg2.png)

1.  請使用調節器將樣本大小下限調整為 100，然後按**下一步**。

    ![大小下限](images/gs-fair-config-sample.png)

    對於本指導教學，樣本大小下限設為 100。一般而言，建議使用較大樣本，以確保樣本不會太小，如果太小會扭曲結果。{: note}

1.  檢閱您的選擇，按一下**儲存**，然後按一下**確定**。

    ![配置摘要](images/fair-summary.png)

    會出現下列視窗，其中提供一個已除去偏誤的評分端點。由於本指導教學使用 GUI 方法（而非 CLI）來對資料評分，如果要繼續，請按一下**確定**。

    ![除去偏誤 API](images/gs-insight-debias-api.png)

### 配置精確度監視
{: #gs-cfgac}

1.  按一下**精確度**。

1.  閱讀有關精確度的說明，並按**下一步**。如需相關資訊，請參閱[精確度](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。

1.  將精確度警示臨界值設為 90%，並按**下一步**。

1.  請在下個畫面上，使用調節器將樣本大小下限調整為 10，然後按**下一步**。

    對於本指導教學，樣本大小下限已設為 10。一般而言，建議使用較大樣本，以確保樣本不會太小，如果太小會扭曲結果。{: note}

1.  在樣本大小上限方面，請使用 10000。按**下一步**。

1.  檢閱您的選擇，按一下**儲存**，然後按一下**確定**。

1.  最後，會呈現一個選項，讓您新增回饋資料，相關說明請見下一節。現在，請按一下**確定**來關閉視窗，而不要按一下**新增回饋資料**按鈕。

    如需詳細資料，請參閱[配置「精確度」監視器](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config)。

## 提供一組樣本回饋資料給您的模型
{: #gs-smpfeed}

為了能夠監視精確度，必須提供回饋資料給您的模型。必須完成此動作，精確度資料才會出現在儀表板中。您可以一併產生要求，作法是將樣本回饋資料新增至模型來進行評分。對於此作業，您將下載含有樣本回饋資料的 CSV 檔案。

1.  下載 [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv) 檔。

1.  在 {{site.data.keyword.aios_short}} 中，按一下**洞察**標籤。

    ![洞察](images/insight-dash-tab.png)

1.  按一下所部署模型的圖磚。

    ![「洞察」標籤 - 無資料](images/gs-insight-overview.png)

1.  然後按一下「編輯」圖示，以編輯部署配置。

    ![顯示「編輯」圖示](images/gs-insight-edit-icon.png)

1.  在「摘要」側邊畫面中，按一下**新增回饋資料**按鈕，並選取您下載的 `credit_feedback_data.csv` 檔。選取**逗點 (,)** 定界字元，然後按一下**確定**。

    檔案大小目前限制為 8 MB。
    {: note}

    ![「精確度」定界字元](images/accuracy-delimit.png)

    新增 CSV 檔案時，會提供回饋資料給您的模型。

    ![「摘要」畫面](images/gs-insight-summary-panel-2.png)

## 檢視結果
{: #gs-viewres}

在您配置精確度監視之後，會在一個小時之後執行精確度檢查。在正式作業系統中，這樣做是合理的，如此您的儀表板就能累積回饋資料。基於本指導教學的目的，您可能希望在新增回饋資料之後手動執行精確度檢查，以便可在**洞察**儀表板中看到結果。

如果要立即檢查結果，請從**洞察**頁面中，選取一項部署，然後按一下**立即檢查公平性**或**立即檢查品質**按鈕。

### 檢視您部署的相關洞察
{: #gs-viewin}

1. 從 [{{site.data.keyword.aios_short}} 儀表板](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}，按一下**洞察**標籤。

  ![洞察](images/insight-dash-tab.png)

1. 檢視「洞察」頁面，以查看已部署模型的度量概觀。如果公平性或精確度度量超出 90% 臨界值，您可以檢視其相關警示。

  「公平性」和「精確度」度量可能需要耗費一個小時才會顯示。{: tip}

  ![「洞察」概觀](images/insight-overview.png)

### 檢視您部署的監視資料
{: #gs-viewmon}

1.  按一下「洞察」頁面上的圖磚，以選取部署。會顯示該項部署的監視資料。附註：在您上傳回饋 .csv 檔之後，您可能發現「公平性」或「精確度」資料未更新。如果要立即檢查結果，請按一下**立即檢查公平性**或**立即檢查品質**按鈕。
1.  在圖表中滑動標記，以選取您執行樣本資料和樣本回饋資料那段時間範圍的資料。然後按一下**檢視明細**。

    ![監視資料](images/insight-monitor-data.png)

1.  接下來，請檢閱您所監視之資料的圖表。就本例而言，請使用**特性**功能表來選取 `Age` 或 `Sex`，以查看受監視資料的相關明細。

    如需如何閱讀這些圖表的相關資訊，請參閱[將特定小時的資料視覺化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。{: tip}

    ![「洞察」概觀](images/insight-review-charts.png)

### 檢視模型交易的可解釋性
{: #gs-viewextx}

1.  針對您所監視的資料，從圖表中按一下**檢視交易**按鈕。

    ![檢視交易](images/view_transactions.png)

1.  會顯示過去一小時造成偏誤的交易清單。如果要針對特定交易，檢視更詳細的解釋，請從**動作**直欄中，按一下**解釋**。

    ![交易清單](images/transaction_list_cr.png)
    
1.  會顯示解釋，指出模型是如何得出其結論。這項解釋包括：模型的信賴度、確信層次的造成因素，以及輸送給模型的直欄。

    ![檢視交易](images/view_transaction1.png)

## 相關資訊
{: #wos-info}

- 如果要瞭解偏誤，請參閱[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)。
- 如果要瞭解您模型預測輸出結果的精準程度，請參閱[精確度](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)。
- 如果要瞭解如何解讀圖表、資料和交易，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。
