---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: accuracy, 

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

# 精確度
{: #acc-monitor}

精確度可讓您知道您模型預測輸出結果的精準程度。
{: shortdesc}

## 瞭解精確度
{: #acc-understand}

視演算法的類型而定，精確度可能意味著各種事項：

- *多類別分類*：精確度會測量任何類別預測正確的次數，並根據資料點的數目來正規化。如需詳細資料，請參閱 Apache Spark 說明文件中的[多類別分類![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window}。

- *二進位分類*：以二進位分類演算法來說，會將精確度當成 ROC 曲線之下的區域來測量。如需詳細資料，請參閱 Apache Spark 說明文件中的[二進位分類![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window}。

- *迴歸*：迴歸演算法是利用「判定係數」（或稱 R2）來測量。如需詳細資料，請參閱 Apache Spark 說明文件中的 [迴歸模型評估 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window}。

### 如何運作
{: #acc-works}

您需要依如下所示，透過 {{site.data.keyword.aios_short}} 使用者介面，使用 [Python 用戶端![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} 或 [Rest API ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}，來新增手動標示的回饋資料。

檢閱[支援的架構](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)，以了解精確度監視限制。

### 除去偏誤後的精確度
{: #acc-debias-view}

當有資料支援它時，模型的精確度會同時包含原始模型和已除去偏誤模型。{{site.data.keyword.aios_full_notm}} 會計算已除去偏誤之輸出的精確度，並在有效負載記載表格中儲存成一個額外的直欄。

![出現模型視覺化，其中同時計算了原始模型和已除去偏誤模型的精確度](images/debiased-accuracy.png)

## 配置「精確度」監視器
{: #acc-config}

1.  從*何謂精確度？*頁面中，按**下一步**，啟動配置處理程序。

    ![「何謂精確度？」頁面](images/accuracy-what-is.png)

1.  在*設定精確度臨界值*頁面上，選取一值來代表可接受的精確度層次。

    精確度是一個值，並且是從每一個特定模型類型相關聯的相關資料科學度量合成而來。評分是一種正規化測量，可讓您輕鬆比較不同模型類型之間的精確度。在一般情況下，精確度評分 80 就已足夠。
{: note}

    ![設定精確度限制](images/accuracy-set-limit.png)

    按**下一步**以繼續。

1.  現在，請設定樣本大小下限和上限。大小下限用來在評估資料集中的可用記錄數目未達下限之前，阻止測量「精確度」；這可確保樣本大小不會太小而扭曲結果。樣本大小上限有助於妥善管理評估資料集時所耗費的時間與心力；如果超過此大小，則只會評估最近的記錄。

     ![配置樣本大小](images/accuracy-config-sample.png)

1.  按**下一步**按鈕。

    會呈現您的選擇摘要，供您檢閱。只要您想變更，請針對該區段按一下**編輯**鏈結。

1.  按一下**儲存**，以完成配置。

現在，會提供選項讓您直接提供回饋資料給模型，以評估其精確度。

  ![傳送回饋資料](images/accuracy-send-feedback0.png)

選取*新增回饋資料*按鈕，以上傳 CSV 格式的資料檔；設定符合您資料的定界字元。

預期回饋 CSV 檔案應具有所有的特性值，以及具有手動指派的目標/標籤值。例如，藥物模型訓練資料含有特性值 `"AGE"`、`"SEX"`、`"BP"`、`"CHOLESTEROL"`、`"NA"`、`"K"`，以及目標/標籤值 `"DRUG"`。回饋 CSV 檔案需要包含那些欄位的值；例如：`[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`。若有針對回饋 CSV 檔案提供標頭，則會使用標頭來對映欄位名稱。否則，欄位順序**必須**與訓練綱目中的順序完全相同。
如需訓練資料的相關資訊，請參閱 [ 為何 {{site.data.keyword.aios_short}} 需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
{: important}

請注意，您模型所傳回的預測類型與回饋資料中的標籤/目標直欄必須相符。
{: note}

  ![「精確度」定界字元](images/accuracy-delimit.png)

檔案大小目前限制為 8MB。
    {: note}

另外，您也可以使用所提供的 `cURL` 或 `Python` 程式碼 Snippet，來發佈回饋資料。

程式碼 Snippet 中的欄位和值需要換成實際值，因為所提供的欄位及值只是範例。
{: important}

您也可以選擇**結束**，來跳過這個選用步驟；之後您仍然能夠上傳 CSV 檔來進行評估。

### 後續步驟
{: #acc-next}

從*配置監視器*頁面，您可以選取另一個監視種類。
