---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# 群組的公平性
{: #quality_group}

群組度量的「公平性」會促使模型傾向交付有利輸出結果給一個群組，而高過另一個群組。群組可以是任何群組，例如：年齡、性別或人種。
{: shortdesc}

## 「群組的公平性」摘要
{: #quality_group-glance}

- **說明**：模型傾向交付有利輸出結果給一個群組而高過另一個群組。
- **預設臨界值**：下限 = 80%
- **預設建議**：您可以使用於商業應用程式中的不偏誤評分端點，用於接收所部署模型的不偏誤回應。
- **問題類型**：全部
- **資料類型**：結構化
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：是

## 受保護屬性
{: #quality_group-atts}

{{site.data.keyword.aios_short}} 會自動識別模型中是否存在任何已知的受保護屬性。當 {{site.data.keyword.aios_short}} 偵測到這些屬性時，它會自動建議針對所存在的每一個屬性，配置偏誤監視器，以確保在正式作業中會追蹤對這些潛在機密屬性的偏誤。 

### 性別
{: #quality_group-sex}

{{site.data.keyword.aios_short}} 建議在**性別**屬性內配置偏誤監視器，以便讓 `Woman` 和 `Non-Binary` 成為受監視值，讓 `Male` 成為參照值。 

### 種族
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} 建議在**種族**屬性內配置偏誤監視器，以便讓 `White-caucasian` 成為參照值，讓其他種族成為受監視值。

### 婚姻狀態
{: #quality_group-marital}

{{site.data.keyword.aios_short}} 建議在**婚姻狀態**屬性內配置偏誤監視器，以便讓 `married` 成為參照值，讓 `single` 成為受監視值。

### 年齡
{: #quality_group-age}

{{site.data.keyword.aios_short}} 建議在**年齡**屬性內配置偏誤監視器，以便讓年齡範圍產生可行的除去偏誤。

### 郵遞區號
{: #quality_group-zip}

{{site.data.keyword.aios_short}} 建議在**郵遞區號**屬性內配置偏誤監視器，以便對個別的郵遞區號評分。

## 解讀顯示畫面
{: #quality_group-display}

### 群組的公平性評分
{: #quality_group-display-fairnessscore}



### 受監視的群組
{: #quality_group-display-monitoredgroups}



### 排程
{: #quality_group-display-schedule}

**排程**窗格顯示 



