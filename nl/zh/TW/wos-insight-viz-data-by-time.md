---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 將特定小時的資料視覺化
{: #it-vdet}

如果要查看特定「公平性」統計資料背後的明細，請針對特定時間，按一下圖表。會開啟視覺化，以顯示受監視特性在所選該小時的資料點。根據前述範例，下列範例中顯示「年齡」特性。
{: shortdesc}

請注意頁面頂端的三個過濾器（特性、日期和小時），這可讓您選擇不同的特性或時間來檢閱明細。

![會顯示時間序列圖表，其中的直欄代表年齡的有效負載和擾動資料，以及有利輸出結果數目](images/wos-insight-data-detail.png)

## 解讀圖表
{: #it-intp}

圖表顯示了很多事項：

- 您可以觀察遇到偏誤的族群（18 歲到 23 歲的客戶）。圖表也會顯示此族群的預期輸出結果百分比。

- 圖表會顯示參照族群的預期輸出結果百分比 (70%)。這是所有參照族群的預期輸出結果平均值。

- 圖表指出存在偏誤，這是因為 18 歲到 23 歲族群之預期輸出結果百分比，與參照族群的預期輸出結果百分比的比率，超出臨界值。換句話說，0.52/0.7 = 0.74，這小於 0.8 臨界值。

- 在分析有效負載表格資料中屬性的每一個值以識別偏誤之後，圖表也會一一顯示每一個特殊值之參照值與受監視值的分佈。換句話說，如果偏誤偵測演算法分析了有效負載表格中最近的 1790 筆記錄，這些記錄中有 120 筆是關於 18 歲到 23 歲的客戶，而在該項分佈中，會以長條圖來代表 `Approved` 和 `Denied` 輸出結果。會針對公平性屬性的每一個特殊值，一一顯示有效負載資料的分佈（即使會顯示參照值）。此資訊可用來使偏誤與模型所收到的資料量產生關聯。

- 此外，圖表也顯示 31 歲到 35 歲族群收到 91% 預期輸出結果。這指明了偏誤的來源，也就是說，此群組中的資料扭曲了結果，而導致參照類別的預期輸出結果百分比增加。此資訊可用來識別資料中的某些部分，以便之後在重新訓練模型時可以減少取樣它們。

- 另一件重要事項是，當表格中的資料已被識別要手動標示時，圖表會顯示該表格的名稱。每當演算法在模型中偵測到偏誤時，它也會識別資料點，以便傳送給人員來手動標示。之後這項手動標示的資料會連同原始的訓練資料，用來重新訓練模型。這個重新訓練過的模型可能就不會有偏誤。手動標示表格存在於 {{site.data.keyword.aios_short}} 實例相關聯的資料庫中。
