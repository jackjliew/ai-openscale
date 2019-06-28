---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 自動設置
{: #wos-fast-start}

如果要快速查看 {{site.data.keyword.aios_short}} 如何監視模型，請執行您在第一次登入 {{site.data.keyword.aios_short}} 使用者介面時，所提供的示範實務選項。請參閱[「使用使用者介面」示範](#wos-work-demo)。
{: shortdesc}

## 開始之前
{: #wos-prereqs}

開始進行導覽之前，您必須已設定下列資源：

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## 「使用使用者介面」示範
{: #wos-work-demo}

1.  登入 {{site.data.keyword.bluemix_full}} 上的 {{site.data.keyword.aios_short}} 實例。
1.  如果要使用示範實務，請按一下**執行示範**。

   ![示範 - 歡迎使用](images/fastpath_demo_11.31.04.png)

   在佈建 {{site.data.keyword.aios_short}} 服務時，您可以檢閱示範實務：

   ![示範預覽](images/fastpath_demo_11.31.58.png)

當佈建完成時，按一下**讓我們開始**按鈕，以導覽 {{site.data.keyword.aios_short}} 儀表板，然後繼續[在 {{site.data.keyword.aios_short}} 中檢視結果](#wos-open)。

   ![示範 - 讓我們開始](images/fastpath_demo_11.33.45.png)


## 在 {{site.data.keyword.aios_short}} 中檢視結果
{: #wos-open}

如果要檢視模型之公平性和精確度的相關洞察、受監視資料的明細，以及個別交易的可解釋性，請開啟 {{site.data.keyword.aios_short}} 儀表板。每一項部署各會顯示成一個磚。此導覽配置了一個稱為 `GermanCreditRiskModel` 的部署，如下列畫面擷取所示：


   ![示範 - 讓我們開始](images/fastpath_demo_11.33.54.png)


### 檢視洞察
{: #wos-insights}

「洞察」頁面會根據所配置的臨界值，顯示公平性和精確度的任何問題，並且一目瞭然。

   ![示範 - 讓我們開始](images/fastpath_demo_11.34.00.png)

### 檢視監視資料
{: #wos-monitoring}

1.  從「洞察」頁面，按一下 `GermanCreditRiskModelICP` 圖磚，以檢視受監視資料的相關明細。
1.  在圖表中按一下並拖曳標記，以檢視某一天和某個時段（這會顯示資料），然後按一下**檢視明細**鏈結。或者，您可以在圖表中按一下不同的時段，來變更您要查看的資料。

     - 例如，下列畫面顯示特定日期和時間的資料。日期和時間會因您執行模組的時間而異。

     - 如需解讀時間序列圖表的相關資訊，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。

   ![示範 - 讓我們開始](images/fastpath_demo_11.34.17.png)

1.  如果要查看 `SEX` 資料監視的相關詳細資料，請確定已從下拉功能表中選取 `SEX`。

    - 請注意，在下列畫面擷取中，有存在偏誤。
    
   ![示範 - 讓我們開始](images/fastpath_demo_11.34.27.png)

    - 如需如何解讀特定小時之資料點圖表的相關資訊，請參閱[資料視覺化](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual)。


### 檢視可解釋性
{: #wos-explain}

如果要瞭解造成特定時段出現偏誤的因素，請從前一節所顯示的視覺化畫面中，按一下**偏誤交易**圓鈕。

   ![示範 - 讓我們開始](images/fastpath_demo_11.35.06.png)

會針對存在偏誤的那些交易，列出其過去一小時的交易 ID。對於此模組中使用的模型，可用的要求有存在偏誤。

   ![示範 - 讓我們開始](images/fastpath_demo_11.35.12.png)

如需尋找及解釋交易的相關資訊，請參閱[監視可解釋性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)。

   ![示範 - 讓我們開始](images/fastpath_demo_11.35.50.png)

## 完成導覽
{: #wos-done-demo}

1. 按一下**完成**按鈕。

   ![示範 - 讓我們開始](images/fastpath_demo_11.37.22.png)

2. 按一下**讓我們開始**按鈕，以開始使用 {{site.data.keyword.aios_short}}。

   ![示範 - 讓我們開始](images/fastpath_demo_11.33.45.png)


## 相關資訊
{: #wos-info}

- 如果要瞭解偏誤，請參閱[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)。
- 如果要瞭解您模型預測輸出結果的精準程度，請參閱[精確度](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)。
- 如果要瞭解如何解讀圖表、資料和交易，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。
