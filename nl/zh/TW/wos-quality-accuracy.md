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

# 精確率
{: #accuracy-opener}

精確度是測量您模型所包含之正確預測的比例。
{: shortdesc}

## 「精確度」摘要
{: #anlz_metrics_supqualdets_acc}

- **說明**：正確預測的比例
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：二進位分類及多類別分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：混淆矩陣


## 瞭解精確度
{: #acc-understand}

視演算法的類型而定，精確度可能意味著各種事項：

- *多類別分類*：精確度會測量任何類別預測正確的次數，並根據資料點的數目來正規化。如需詳細資料，請參閱 Apache Spark 說明文件中的[多類別分類](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external}。

- *二進位分類*：以二進位分類演算法來說，會將精確度當成 ROC 曲線之下的區域來測量。如需詳細資料，請參閱 Apache Spark 說明文件中的[二進位分類](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external}。

- *迴歸*：迴歸演算法是利用「判定係數」（或稱 R2）來測量。如需詳細資料，請參閱 Apache Spark 說明文件中的 [迴歸模型評估](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external}。

### 如何運作
{: #acc-works}

您需要依下列範例所示，透過 {{site.data.keyword.aios_short}} 使用者介面，使用 [Python 用戶端](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external}或 [Rest API](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}，來新增手動標示的回饋資料。

### 已除去偏誤的精確度
{: #acc-debias-view}

當有資料支援它時，會同時計算原始模型與已除去偏誤模型的精確度。{{site.data.keyword.aios_full_notm}} 會計算已除去偏誤之輸出的精確度，並在有效負載記載表格中儲存成一個額外的直欄。

![出現模型視覺化，其中同時計算了原始模型和已除去偏誤模型的精確度](images/debiased-accuracy.png)
