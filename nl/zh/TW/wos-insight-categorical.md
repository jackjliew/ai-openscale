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

# 解釋種類模型
{: #ie-class}

這個可解釋性範例指的是一個二進位分類模型，用來核准或拒絕保險理賠。在本例中，您可以看到正面或負面造成 `DENIED` 最終輸出結果的一些因素。
{: shortdesc}

值為 `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` 的*原則歷時*特性在決定了 DENIED 輸出結果的模型中，所造成的影響最大。造成此輸出結果的其他特性還有*理賠頻率* (`High`) 和*年齡* (`18`)，以及僅帶來些微影響的*汽車價格* (`$50,000`)。

![顯示可解釋性二進位分類，其中提供拒絕及核准理賠的相關明細](images/insight-explain-binary.png)

儘管在決定交易的輸出結果時，圖表有助於顯示最重要的因素，分類模型也可以包含進階解釋，且這些解釋詳述於 `Minimum changes for Approved outcome` 和 `Minimum changes for this outcome` 區段中。

進階解釋不適用於迴歸、影像和非結構化文字模型。
{: note}

`Minimum changes for Approved outcome` 指出，如果特性的值已變更為此區段所列出的值，則模型的預測將會變更。

同樣地，`Minimum changes for this outcome` 指出，即使特性的值已變更為此區段所列出值，模型的預測並未變更。

因此由這兩個值可看出，模型在要產生解釋之資料點附近的行為。

![可解釋性二進位分類明細，其中含有若要變更輸出結果，所需進行的最小變更](images/insight-explain-binary2.png)
