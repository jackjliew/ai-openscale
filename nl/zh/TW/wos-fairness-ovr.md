---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 公平性度量概觀
{: #anlz_metrics_fairness}

使用 {{site.data.keyword.aios_full}} 公平性監視，來判斷您的模型所產生的輸出結果，對於受監視群組是否公平。啟用公平性監視時，依預設，它會每小時產生一組度量。您可以藉由按一下**立即檢查品質**按鈕或利用 Python 用戶端，以隨需應變方式產生這些度量。
{: shortdesc}

{{site.data.keyword.aios_short}} 會自動識別模型中是否存在任何已知的受保護屬性。當 {{site.data.keyword.aios_short}} 偵測到這些屬性時，它會自動建議針對所存在的每一個屬性，配置偏誤監視器，以確保在正式作業中會追蹤對這些潛在機密屬性的偏誤。 

目前，{{site.data.keyword.aios_short}} 會偵測是否存在下列的受保護屬性，並建議使用監視器： 

- 性別
- 種族
- 婚姻狀態
- 年齡
- 郵遞區號

除了偵測受保護屬性，{{site.data.keyword.aios_short}} 還會建議應將每一個屬性內的哪些值設為受監視和參照值。因此，舉例來說，{{site.data.keyword.aios_short}} 建議在「性別」屬性內配置偏誤監視器，以便讓 "Woman" 和 "Non-Binary" 成為受監視值，讓 "Male" 成為參照值。如果您想變更任何建議，可以透過偏誤配置畫面來編輯它們。 

建議的偏誤監視器有助於加快配置，並確保您會檢查 AI 模型的機密屬性是否公平。由於監管者開始密切注意演算上的偏誤，對於組織，清楚瞭解其模型如何執行，以及針對特定群組所產生的輸出結果是否不公平，就變得很重要。

## 瞭解公平性
{: #mf-understand}

{{site.data.keyword.aios_short}} 會在執行時期檢查所部署模型的偏誤。如果要偵測所部署模型的偏誤，您必須定義公平性屬性（例如「年齡」或「性別」），如下列[配置「公平性」監視器](#mf-config)一節中所詳述。

請務必在 {{site.data.keyword.pm_short}} 中，指定模型或函數的輸出綱目，才能在 {{site.data.keyword.aios_short}} 中啟用偏誤檢查。您可以在 `store_model` API 的 meta 資料部分中，使用 `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` 內容來指定輸出綱目。如需相關資訊，請參閱 [{{site.data.keyword.pm_full}} 用戶端說明文件](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}。

### 如何運作
{: #mf-works}

在您配置「公平性」監視器之前，有一些重要的概念務必要瞭解。

- 公平性屬性是指模型有可能顯現偏誤的模型屬性。以公平性屬性 **`Gender`** 為例，模型可能對於特定的性別值（`Female`、`Transgender` 等）有偏誤。另以公平性屬性 **`Age`** 為例，模型可能對於某年齡群（例如 `18 to 25`）的人群顯現偏誤。

- 參照值和受監視值：公平性屬性的值分成兩個不同的種類：「參照」和「受監視」。「受監視」值是指要作為判別對象的那些值。對於 **`Gender`** 等之類的公平性屬性而言，「受監視」值可以是 `Female` 和 `Transgender`。對於 **`Age`** 等之類的數值型公平性屬性而言，「受監視」值可以是 `[18-25]`。給定公平性屬性的其他所有值則可視為參照值，例如 `Gender=Male` 或 `Age=[26,100]`。

- 有利和不利輸出結果：模型的輸出會分類成「有利」或「不利」。舉例來說，如果模型預測某人是否應取得貸款，則「有利」輸出結果可以是 `Loan Granted` 或 `Loan Partially Granted`，而「不利」輸出結果可能是 `Loan Denied`。因此，「有利」輸出結果就是被視為正面輸出結果的那一個，而「不利」輸出結果則被視為負面。

{{site.data.keyword.aios_short}} 演算法會使用有效負載記載表格中所呈現的最近 `N` 筆記錄，每小時計算一次偏誤；`N` 值是在配置「公平性」時指定的。演算法會擾動這最近 `N` 筆記錄，以產生額外的資料。

擾動的作法是將公平性屬性的值從「參照」變更為「受監視」，反之亦然。之後會將擾動資料傳送給模型，以評估其行為。演算法會查看有效負載表格中的最近 `N` 筆記錄，以及查看模型在擾動資料上的行為，來決定模型是否以偏誤的方式執行。

在這個組合的資料集中，如果「受監視」類別的「有利」輸出結果百分比，小於「參照」類別的「有利」輸出結果百分比達到某個臨界值，就會將該模型視為有偏誤。此臨界值是在配置「公平性」時指定的。

公平性值可以超過 100%。這表示「受監視」群組所收到的有利輸出結果超過「參照」群組。此外，只要沒有傳送任何新的評分要求，「公平性」值會維持不變。
{: note}

### 數學計算
{: #mf-bias-math}

{{site.data.keyword.aios_short}} 中使用的公平性度量是差別影響，這是比對特權群組收到特定輸出結果或結果的比率，來測量無特權群組收到相同輸出結果或結果的比率。

下列數學公式用來計算差別影響：

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
差別影響 =         ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

其中，`num_positives` 是群組中收到正面輸出結果的個體數目（privileged=False，代表無特權；privileged=True，代表特權），num_instances 是群組中的個體總數。

產生的數字是一個百分比，亦即，非特許群組收到正面輸出結果，佔特許群組收到正面輸出結果的比率。例如，例如，如果信用風險模型將「無風險」預測指派給 80% 的非特許申請者，以及指派給 100% 的特許申請者，則該模型的差別影響（在 {{site.data.keyword.aios_short}} 中會呈現成公平性評分）為 80%。

在 {{site.data.keyword.aios_short}} 中，正面輸出結果會指定成有利輸出結果，負面輸出結果會指定成「不利」輸出結果。特許群組會指定成參照群組，非特許群組則指定成受監視群組。


### 偏誤視覺化 ![測試版標記](images/beta.png)
{: #mf-monitor-bias-viz}

當偵測到潛在的偏誤時，{{site.data.keyword.aios_short}} 會執行一些功能，來確認該偏誤是否是真的。{{site.data.keyword.aios_short}} 會擾動資料，其作法是將受監視值翻轉成參照值，然後透過模型執行這筆記錄。接著，它會將產生的輸出顯現成已除去偏誤的輸出。{{site.data.keyword.aios_short}} 也會訓練一個已除去偏誤的投影模型，然後用它來偵測模型何時做出有偏誤的預測。 

會使用兩個不同的資料集來計算公平性和精確度。公平性是以「有效負載 + 擾動資料」來計算。精確度是以回饋資料來計算。為了計算精確度，{{site.data.keyword.aios_short}} 需要手動標示資料，這只會呈現在回饋表格中。

這些判定的結果會提供於偏誤視覺化中，其中包含下列視圖。（必須要有支援資料，才能看見這些視圖）

- **有效負載 + 擾動**：如果未符合評估所需的最低記錄數目，則包含所選那個小時內所收到的評分要求，外加過去幾個小時內的其他記錄。如果受監視特性的值有變更，會包含用來測試模型回應的其他擾動/合成記錄。

   請留意下列的有效負載和擾動明細：

   - 在這個小時內從有效負載表格讀取的記錄數目
   - 從過去幾個小時所讀取的其他記錄（例如，如果公平性配置中的 `min_records` 值設為 1000，而下午 2 點到 3 點之間只新增了 10 筆記錄，為了符合最低需求，系統會從過去幾個小時額外讀取 990 筆記錄。）
   - 各公平性屬性的擾動記錄
   - 必須計算其偏誤之資料框架中最舊記錄的時間戳記
   - 必須計算其偏誤之資料框架中最新/最近記錄的時間戳記

  ![有效負載外加擾動的範例](images/payload&perturbed.png)



- **有效負載**：模型在所選那個小時內所收到的實際評分要求。

   請留意下列的有效負載明細：
   
   - 已從有效負載表格讀取/對其執行除去偏誤作業的記錄數
   - 必須計算其偏誤之資料框架中最舊記錄的時間戳記
   - 必須計算其偏誤之資料框架中最新/最近記錄的時間戳記


  ![有效負載資料範例](images/payload.png)

- **訓練**：用來訓練模型的訓練資料記錄。

   請留意下列的訓練明細：
   
   - 訓練資料記錄數目。訓練資料會讀取一次，並將分佈儲存在 `subscription/fairness_configuration` 變數中。在計算分佈期間，我們也應會找到訓練資料記錄數目，並將它儲存在相同的分佈中。此外，當訓練資料變更時（表示是否再次執行 `POST /data_distribution` 指令），會在 `fairness_configuration/training_data_distribution` 變數中更新此值。在傳送度量期間，我們應該也會傳送此值。
   - 前次處理（第一次和後續的更新）訓練資料的時間

  ![訓練資料範例](images/training.png)
   

   
- **除去偏誤**：處理執行時期和擾動資料之後的除去偏誤演算法的輸出。選取**除去偏誤**圓鈕時，會顯示相對於正式作業中的模型，除去偏誤模型中的變更。圖表會反映群組的輸出結果狀態已改進。


   請留意下列的除去偏誤明細：
   
   - 已從有效負載表格讀取/對其執行除去偏誤作業的記錄數
   - 為執行偏誤而讀取，從而已除去偏誤的其他記錄。會與`有效負載 + 擾動`選擇項中的數目相同
   - 各公平性屬性的擾動記錄
   - 必須計算其偏誤之資料框架中最舊記錄的時間戳記
   - 必須計算其偏誤之資料框架中最新/最近記錄的時間戳記
   - 前後公平性值會顯示在「已除去偏誤」視圖的標頭部分中 
      - **後**精確度的計算方式是，取得回饋表格中的資料，並傳送給作用中的除去偏誤 API。此 API 會傳回已除去偏誤的預測。回饋資料也會包含手動標籤。手動標籤會與已除去偏誤的預測相互比較，以計算精確度。此 API 會傳回已除去偏誤的預測。回饋表格也會包含手動標籤。手動標籤會與已除去偏誤的預測相互比較，以計算精確度。 
      - **前**精確度是以相同的回饋資料來計算。就前精確度的計算來說，會傳送回饋資料給模型，以取得其預測，並將預測值與手動標籤相互比較，以取得精確度。

  ![除去偏誤資料範例](images/debiased.png)
  
### 範例
{: #mf-ex1}

假設有一個資料點，其中 `Gender=Male`（「參照」值），模型預測為「有利」輸出結果，但是當將 `Gender` 變更為 `Female`（「受監視」值），來擾動記錄時，儘管其他所有的特性值都維持相同，模型卻預測為「不利」輸出結果。如果資料點足夠（有效負載表格中的最近 `N` 筆記錄，外加擾動資料），但模型在這些資料點中卻以偏誤的方式執行，則該模型整體來說是顯現偏誤。

### 支援的模型
{: #mf-supmo}

 {{site.data.keyword.aios_short}} 只支援對那些模型以及預期其特性向量中存在某種結構化資料的 Python 函數，執行偏誤偵測。

公平性度量是根據下列資訊來計算：

- 評比有效負載資料。

為了達到適當的監視目的，每個評分要求都應該記載在 {{site.data.keyword.aios_short}} 中。對於 {{site.data.keyword.pm_full}} 引擎，會自動進行有效負載資料記載。

對於其他機器學習引擎，可以使用 Python 用戶端或 REST API 來提供有效負載資料。

對於 {{site.data.keyword.pm_full}} 以外的機器學習引擎，公平性監視會在受監視部署上建立其他評分要求。
{: note}

您可以在 {{site.data.keyword.aios_short}} 儀表板上檢閱一段時間的所有度量值：

![公平性度量圖表，顯示漂移低於所設定的臨界值](images/fairness_metrics_001.png)

您可以檢閱相關詳細資料，例如有利和不利的輸出結果：

![公平性詳細資料](images/fairness_metrics_002.png)

您可以檢視詳細交易：

![公平性圖表，顯示交易清單](images/fairness_metrics_003.png)

您可以檢視所建議的不偏誤評分端點：

![不偏誤評分端點的詳細資料](images/fairness_metrics_004.png)

### 支援的公平性度量
{: #anlz_metrics_supfairmets}

{{site.data.keyword.aios_short}} 支援下列公平性度量：

- [群組的公平性](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

{{site.data.keyword.aios_short}} 支援下列的受保護屬性： 

- [性別](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [種族](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [婚姻狀態](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [年齡](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [郵遞區號](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### 支援的公平性詳細資料
{: #anlz_metrics_supfairdets}

{{site.data.keyword.aios_short}} 支援公平性度量的下列詳細資料：

- 每一個群組的有利百分比
- 所有公平性群組的公平性平均值

```
                          (受監視群組中的有利輸出結果 %)
差別影響率 =             ____________________________________________
                          (參照群組中的有利輸出結果 %)
```

- 每一個受監視群組的資料分佈
- 有效負載資料的分佈
