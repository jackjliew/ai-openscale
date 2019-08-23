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

# 檢視部署的資料
{: #it-vdep}

請從儀表板中選取一項部署，以查看該部署的監視資料。標題顯示所部署模型的相關資訊，例如：**模型 ID** 和**建立日期**欄位。
{: shortdesc}

![顯示時間序列圖表，其中顯示一天中的數個小時，以及一個公平性評分](images/insight-time-chart.png)

由於演算法只會每小時執行一次，也會提供一些鏈結，讓您隨需檢查公平性和品質。從**排程**畫面中，您可以按一下下列鏈結，以立即檢查您的資料：

![顯示「檢查公平性」按鈕](images/wos-fairness-button.png)


![顯示「檢查品質」按鈕](images/wos-quality-button.png)

接下來，請按一下圖表，並在圖表中移動標記，以查看某個小時的統計資料。

![顯示時間序列圖表明細，其中，在圖表中選取了特定的資料點，且其中的工具提示指出按一下以檢視明細](images/wos-insight-time-detail.png)

- ***公平性***：「性別」和「年齡」這兩個「公平性」特性符合其核准臨界值。
- ***品質***：**ROC 下方的區域**度量顯示警示，因為它不在所配置的臨界值內。
- ***每分鐘的平均要求數***：按一下**傳輸量**度量，以查看每分鐘處理的記錄數。傳輸量每分鐘會計算一次，且會在圖表中報告其在一整個小時內的平均值。


## 檢視交易
{: #it-tra}

當您按一下**檢視交易**按鈕時，這個選項可讓您檢視造成偏誤的個別交易。

![顯示「檢視交易」按鈕](images/view_transactions.png)

會列出以偏誤的方式執行部署的交易清單。請針對任何交易 ID，按一下**解釋**鏈結，以便在「可解釋性」標籤中取得該交易的相關明細。如需相關資訊，請參閱[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

選取**所有交易**視圖，以查看所選特性（在本例中為「年齡」）以及所選週期（在本例中為「2018 年 9 月 15 日 1:00 PM」）的所有交易：

![交易會列出特定資料點的所有交易](images/transaction_list1.png)

選取**偏誤交易**視圖，以便只查看收到偏誤輸出結果的交易子集。每一項偏誤交易會與類似但略作改變（擾動）的交易比較，以顯示一旦變更受監視特性（年齡）的值時，會為該偏誤交易帶來怎樣的有利輸出結果：

![交易只列出偏誤的交易](images/transaction_list2.png)


