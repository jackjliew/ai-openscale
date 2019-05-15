---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

您可以透過 {{site.data.keyword.aios_short}} 儀表板，來追蹤您正在監視的所有部署。儀表板是您檢視 {{site.data.keyword.aios_short}} 的主視圖。儀表板由五個標籤組成：

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

**解釋交易**標籤 (![「解釋交易」標籤](images/insight-transact-tab.png) )可讓您搜尋特定的交易 ID，以解釋特定的部署交易。如需相關資訊，請參閱[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

## AI 工具
{: #io-too}

**AI 工具**標籤 (![「AI 工具」標籤](images/aitools.png)) 會開啟對話框，其中提供指向其他 IBM AI 工具選項的鏈結：

- *[Watson Studio Lite 方案 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*：Watson Studio 為您提供環境和工具，來分析資料並加以視覺化、清理及體現資料、汲取串流資料，或是建立、訓練及部署機器學習模型。請按一下「註冊取得免費 Watson Studio Lite 方案」鏈結，以取得 Watson Studio。

- *[NeuNetS ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}*（*測試版*）：Neural Network Synthesizer（或 "NeuNetS"）目前是測試版，可讓您使用 Watson Studio 中的 {{site.data.keyword.aios_short}} 技術來合成 AI 模型。請按一下「合成模型」按鈕，以使用 NeuNetS。

  ![NeuNetS 對話框](images/neunets-dialog.png)

## 「說明」標籤
{: #io-help}

「說明」標籤 (![「交易」標籤](images/insight-help-tab.png)) 提供其他資訊，來協助您使用 {{site.data.keyword.aios_short}}。
