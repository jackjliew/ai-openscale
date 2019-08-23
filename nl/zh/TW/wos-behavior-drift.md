---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# 漂移幅度 ![測試版標記](images/beta.png)
{: #behavior-drift-ovr}

模型中某些特性的重要性和影響，會隨時間而變更。這會影響相關聯的應用程式和產生的商業結果。透過漂移偵測，{{site.data.keyword.aios_short}} 讓您能夠追蹤模型度量、模型效能，以及特性的加權如何隨著時間而變更。
隨著資料變更，模型做出精確預測的能力可能會降低。漂移幅度是指預測效能隨時間而降低的程度。請使用漂移的相關資訊，以採取更正動作。
{: shortdesc}

## 瞭解漂移偵測
{: #behavior-drift-understand}

漂移是指因隱藏的環境定義，使得預測效能隨時間而下降。由於您的資料會隨時間而變更，模型做出精確預測的能力可能會降低。{{site.data.keyword.aios_short}} 既會偵測也會突顯漂移，以致於您可以採取更正動作。


### 如何運作
{: #behavior-drift-works}

{{site.data.keyword.aios_short}} 會分析所有交易，以尋找促成漂移的交易。接著它會根據明顯促成漂移的屬性值，將記錄加以分組。

### 數學計算
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} 每三個小時會計算一次漂移，亦即，它會分析您預測模型已經分析的相同訓練資料。接著，它會將結果與模型的預測做一比較。當發現變更或不一致時，{{site.data.keyword.aios_short}} 會計算漂移的程度，並根據您設定的臨界值，警示您發生之處。 


### 漂移視覺化
{: #behavior-drift-display}

漂移視覺化同時包含圖形和數值統計資料。

![公平性度量圖表，顯示漂移低於所設定的臨界值](images/drift-example.png)

當按一下圖表時，可以顯示促成漂移的特定交易。會顯示所偵測到之漂移的首要原因，並提供以自然語言說明的觀察，以及一份非預期值清單。

![公平性度量圖表，顯示漂移低於所設定的臨界值](images/drift-detection-example.png)

交易明細畫面中會提供漂移交易，您可以按一下其中的**解釋**，瞭解特定的交易如何將它歸類在漂移種類：

![公平性度量圖表，顯示漂移低於所設定的臨界值](images/drift-detection-transactions.png)


## 後續步驟

- 如需如何設置漂移偵測的相關資訊，請參閱[配置漂移偵測監視器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。
- 如果要減輕漂移，在 Watson OpenScale 偵測到漂移之後，您必須建置新版本的模型，來修正問題。理想的下手點是一些強調顯示成漂移原因的資料點。在您手動標示漂移的交易之後，請在預測模型中引進新的資料，然後使用它們來重新訓練模型。


