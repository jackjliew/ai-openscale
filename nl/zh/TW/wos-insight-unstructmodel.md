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

# 解釋非結構化文字模型
{: #ie-unstruct}

{{site.data.keyword.aios_short}} 支援非結構化文字資料的可解釋性。
{: shortdesc}

## 使用非結構化文字模型
{: #ie-unstruct-steps}

1. 設置您的環境。
   2. 安裝 {{site.data.keyword.aios_short}} 和 {{site.data.keyword.pm_full}} 套件。
   3. 配置您的認證。
   4. 安裝建立模型及進行分析所需的程式庫。這些程式庫包括：
      - `pandas`
      - `pyspark`（如果沒有使用 {{site.data.keyword.DSX}}）

1. 建立及部署您的影像型模型。
   2. 將訓練資料載入至 pandas 框架。
   2. 在資料上訓練模型。
   3. 發佈模型。
   4. 部署模型並進行評分。

7. 指派 `APIClient`，訂閱資產，並對模型評分，以便配置 {{site.data.keyword.aios_short}}。
8. 配置可解釋性。
   9. 啟用可解釋性。
   10. 取得交易的解釋。

## 解釋非結構化文字的交易
{: #ie-unstruct-xplan}

下列的可解釋性範例顯示用來評估非結構化文字的分類模型。解釋顯示對模型預測造成正面及負面影響的關鍵字。我們也會針對原始文字中被當成輸入輸送給模型的識別關鍵字，顯示其位置。

![會顯示可解釋性影像分類圖。其中顯示非結構化文字的信賴度層次。](images/insight-explain-text.png)

## 非結構化文字模型範例
{: #ie-unstruct-ntbkssample}

請使用下列記事本，查看詳細的程式碼範例，並開發您自己的 {{site.data.keyword.aios_short}} 部署：

- [指導教學：產生文字型模型的說明](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

