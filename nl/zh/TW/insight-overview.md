---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 導覽儀表板
{: #io-ov}

您可以透過 {{site.data.keyword.aios_short}} 儀表板，來追蹤您正在監視的所有部署。儀表板是您檢視 {{site.data.keyword.aios_short}} 的主視圖。儀表板由下列標籤組成：

  ![「洞察」標籤](images/insight-tabs.png)

{: shortdesc}

## 洞察
{: #io-ins}

**洞察**標籤 (![「洞察」儀表板](images/insight-dash-tab.png)) 提供高階視圖來監視您的部署。

  ![「洞察」儀表板](images/insight-dashboard.png)

- ***受監視的部署*** - 在本例中，正在監視的部署總計有 10 項。10 項部署中有 8 項顯示在下方的個別圖磚中。

- ***「精確度」警示*** - 總計有 3 則「精確度」警示呈現在下方的圖磚中，並塗上紫色陰影。在本例中，`Driver Performance`、`Market Analytics` 和 `Pricing Risk` 部署顯示的「精確度」值分別是 `60%`、`65%` 和 `79%`。

- ***「公平性」警示*** - 總計有 6 則「公平性」警示呈現在下方的圖磚中，會塗上紫色陰影，且有一個 `BIAS` 小標籤。在本例中，`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization` 和 `Damage Cost Estimator` 部署顯示的「公平性」值分別是 `59%`、`68%`、`62%`、`64%`、`79%` 和 `63%`。

每一個圖磚都會提供該部署的監視活動摘要。請注意，`Call Center Routing` 部署圖磚顯示沒有任何問題，表示這是一個相當穩定且精確的模型。

### 後續步驟
{: #io-next}

選取任何個別的部署圖磚，以檢視該部署的詳細資料。如需相關資訊，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale?topic=ai-openscale-it-ov)和[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

## 配置
{: #io-conf}

**配置**標籤 (![「配置」標籤](images/insight-config-tab.png)) 會針對選取的部署，開啟「配置摘要」。

  ![配置摘要](images/insight-config-summary.png)

在這裡，您可以直接編輯部署監視器的配置設定。

## 交易
{: #io-tran}

使用**解釋交易**標籤（![「解釋交易」標籤](images/insight-transact-tab.png)）來搜尋特定交易 ID，以解釋特定部署交易。如需相關資訊，請參閱[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

## 「說明」標籤
{: #io-help}

「說明」標籤 (![「交易」標籤](images/insight-help-tab.png)) 提供其他資訊，來協助您使用 {{site.data.keyword.aios_short}}。
