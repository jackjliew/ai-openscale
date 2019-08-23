---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# 利用 {{site.data.keyword.aios_short}} 深入洞察
{: #io-ov}

您可以透過 {{site.data.keyword.aios_full}} 儀表板，來追蹤您正在監視的所有部署。儀表板是您檢視 {{site.data.keyword.aios_short}} 的主視圖，可讓您藉以深入洞察您模型的執行方式。
{: shortdesc}

## 洞察
{: #io-ins}

**洞察**標籤 (![「洞察」儀表板](images/insight-dash-tab.png)) 提供高階視圖來監視您的部署。

  ![「洞察」儀表板](images/insight-dashboard.png)

- ***受監視的部署*** - 在本例中，正在監視的部署總計有 10 項。下列 10 項部署中有 8 項顯示在個別的圖磚中。

- ***「品質」警示*** - 總計有 3 則「品質」（舊稱「精確度」）警示呈現在下列圖磚中。在本例中，`Driver Performance`、`Market Analytics` 和 `Pricing Risk` 部署顯示的「精確度」值分別是 `60%`、`65%` 和 `79%`。

- ***「公平性」警示*** - 總計有 6 則「公平性」警示呈現在下列圖磚中，且有一個 `BIAS` 小標籤。在本例中，`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization` 和 `Damage Cost Estimator` 部署顯示的「公平性」值分別是 `59%`、`68%`、`62%`、`64%`、`79%` 和 `63%`。

每一個圖磚都會提供該部署的監視活動摘要。請注意，`Call Center Routing` 部署圖磚顯示沒有任何問題，表示這是一個相當穩定且精確的模型。


## 公平性、品質、效能、精確度和分析洞察
{: #it-ov}

選取任何個別的部署圖磚，以檢視該部署的詳細資料。會以一系列圖表來顯示個別部署的監視資料。這些圖表會追蹤度量，例如：公平性、每分鐘的平均要求數，以及精確度，並且達數天、數週或數個月之久。

- [檢視部署的資料](/docs/services/ai-openscale?topic=ai-openscale-it-vdep)
- [將特定小時的資料視覺化](/docs/services/ai-openscale?topic=ai-openscale-it-vdet)
- [公平性](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)
- [品質](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)
- [漂移](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
- [效能](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_performance)
- [分析](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)
- [除去偏誤選項](/docs/services/ai-openscale?topic=ai-openscale-it-dbo)

## 可解釋性
{: #io-tran}

使用**解釋交易**標籤（![「解釋交易」標籤](images/insight-transact-tab.png)）來搜尋特定交易 ID，以解釋特定部署交易。

- [解釋交易](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)
- [解釋種類模型](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [解釋影像模型](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [解釋非結構化文字模型](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [對比解釋](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)

## 後續步驟
{: #io-next}

- [新增更多部署來監視](/docs/services/ai-openscale?topic=ai-openscale-dpl-select)。

