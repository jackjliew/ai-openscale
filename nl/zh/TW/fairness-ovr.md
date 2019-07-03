---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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
