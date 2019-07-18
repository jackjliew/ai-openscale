---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# 配置公平性監視器
{: #mf-monitor}

在 {{site.data.keyword.aios_full}} 中，公平性監視器會掃描您的部署是否有偏誤，以確保不同族群之間的輸出結果是公平的。
{: shortdesc}

## 步驟
{: #mf-config}

從**公平性**標籤，在**何謂公平性？**頁面中，按一下**開始**，啟動配置處理程序。

![「何謂公平性？」頁面](images/fair-what-is.png)

在這項處理程序中，{{site.data.keyword.aios_full}} 會分析您的模型，並根據最合邏輯的輸出結果提供建議。在**公平性**標籤的後續頁面中，您必須執行下列作業：

1. 選取要監視的特性。只支援種類、數值（整數）、浮點或倍精準數公平性資料類型的特性。不支援其他資料類型的特性。
    

1. 指定參照和受監視群組。

   每一項特性都有特定的需求要配置。例如，如果您選擇 `age` 作為其中一項受監視的特性，您必須直接在**參照群組**和**受監視群組**中輸入值，以定義每一個群組的年齡範圍。

1.  針對特性，設定公平性警示臨界值。

    「公平性」臨界值用來指定相較於「參照」群組的「有利」輸出結果百分比，對於「受監視」群組的「有利」輸出結果百分比，所能接受的差異。

    假設模型會預測何人應取得貸款 (`favorable outcome=loan granted`)，何人不應取得貸款 (`unfavorable outcome=loan denied`)。再者，年齡的「受監視」值是 `[18,25]`，「參照」值是 `[26,100]`。當執行偏誤偵測演算法時，如果發現在最近 `N` 筆記錄外加擾動資料中，年齡群 `[18,25]` 之人群的「有利」輸出結果百分比是 `50%`，而年齡群 `[26,100]` 之人群的「有利」輸出結果百分比是 `70%`，則所算出的「公平性」會是 50*100/70 = 71.42。

    如果「公平性」臨界值設為 80%，則演算法會將模型標示為有偏誤，這是因為所算出的「公平性」超出臨界值。不過，如果臨界值設為 70%，就不會將模型報告為有偏誤。

     您在這些畫面中輸入的值，應會成為要傳送給模型評分端點的值（因而會新增至有效負載表格中）。如果資料在傳送給評分端點之前會先進行操作，請輸入操作後的值。例如，如果原始資料的 *Gender* 值是 `Male` 和 `Female`，且經過操作，以致於傳送給評分端點的資料是 `M` 和 `F`，請在此畫面上輸入 `M` 和 `F`。

1.  請指定一些值來代表模型的有利輸出結果。如果模型輸出綱目含有對映直欄，則這些值是衍生自[訓練資料](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)中的 `label` 直欄。在 {{site.data.keyword.pm_full}} 中，`prediction` 直欄一律具有倍精準數值。對映直欄用來指定這個 `prediction` 值指向類別標籤的對映。

    例如，如果 `prediction` 值是 `1.0`，對映直欄的值可能是 `Loan denied`；這意味著模型的預測是 `Loan denied`。因此，如果模型輸出綱目包含對映直欄，請使用對映直欄中的值來指定「有利」值和「不利」值。

    不過，如果模型輸出綱目中沒有對映直欄，則需要使用 `prediction` 直欄的值（`0.0`、`1.0` 等）來指定「有利」值和「不利」值。

1.  最後，設定樣本大小下限，以便在評估資料集中的可用記錄數目未達下限之前，阻止測量「公平性」。這是確保樣本大小不會太小而扭曲結果。每當執行偏誤檢查時，會使用樣本大小下限來決定將執行偏誤計算的記錄數目。

    會呈現您的選擇摘要，供您檢閱。只要您想變更，請針對該區段按一下**編輯**鏈結，否則，請按一下**儲存**。

    您也可以按一下**新增另一項特性**，回到特性選擇畫面，並將其他特性（例如 `City`、`Zip Code` 或 `Account Balance`）新增至「公平性」監視器。

### 瞭解除去偏誤如何運作
{: #mf-debias}

如果要檢查除去偏誤端點，請按一下**除去偏誤端點**按鈕。然後以不同格式（例如：cURL、Java 或 Python）來檢視及複製端點。 

已除去偏誤的評分端點可完全當成所部署模型正常的評分端點使用。除了傳回所部署模型的回應之外，還會傳回 `debiased_prediction` 和 `debiased_probability` 直欄。

- `debiased_prediction` 直欄含有已除去偏誤的預測值。對 {{site.data.keyword.pm_full}} 而言，這是以編碼方式來表示預測。例如，如果模型預測是 "Loan Granted" 或 "Loan Denied"，{{site.data.keyword.pm_full}} 可將這兩個值分別編碼成 "0.0" 和 "1.0"。`debiased_prediction` 直欄含有這類以編碼方式來表示已除去偏誤的預測。

- 在另一方面，`debiased_probability` 直欄代表已除去偏誤之預測的機率。這是一個倍精準數值陣列，其中，每一個值各代表已除去偏誤之預測（屬於其中一個預測類別）的機率。

假設您的輸出綱目中有一個直欄，且該直欄含有一個 `modeling-role` 設為 `decoded-target` 的直欄，也會傳回另一個直欄 `debiased_decoded_target`。

- `debiased_decoded_target` 直欄會以字串來表示已除去偏誤的預測。在上述範例中，預測值是 "0.0" 或 "1.0"，`debiased_decoded_target` 將包含 "Loan Granted" 或 "Loan Denied"。

理論上，您會從正式作業應用程式直接呼叫此端點，而不是直接呼叫部署在模型處理引擎（{{site.data.keyword.pm_full}}、Amazon Sagemaker、Microsoft Azure ML Studio 等）中之模型的評分端點。這樣一來，{{site.data.keyword.aios_short}} 也會將 `debiased` 值儲存在您模型部署的有效負載記載表格中。之後，凡是透過此端點來完成的評分都會自動除去偏誤。

由於此端點會處理執行時期偏誤，它會繼續對有效負載記載表格中的最新評分資料執行背景檢查，並持續更新偏誤減輕模型（此模型用來去除所傳送之評分要求的偏誤）。在此情況下，{{site.data.keyword.aios_short}} 一律保有最新的送入資料，且其在偵測及減輕偏誤的行為上也會保持最新。

最後，{{site.data.keyword.aios_short}} 使用臨界值決定該資料現在是可接受的，且可視為無偏誤。對於在「公平性」監視器中設定給所配置之所有公平性屬性的臨界值中，會以該臨界值作為最小值。

## 後續步驟
{: #mf-next}

從**配置監視器**頁面，您可以選取另一個監視種類。
