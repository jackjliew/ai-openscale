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

# 解釋影像模型
{: #ie-image}

{{site.data.keyword.aios_short}} 支援影像資料的可解釋性。
{: shortdesc}

## 使用影像模型
{: #ie-image-working}

1. 設置您的環境。
   2. 安裝 {{site.data.keyword.aios_short}} 和 {{site.data.keyword.pm_full}} 套件。
   3. 配置您的認證。
   4. 安裝建立模型及進行分析所需的程式庫。這些程式庫包括：
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. 建立及部署您的影像型模型。
   2. 根據您的分類方式，為影像建立資料夾。
       - 在 `data` 主目錄內，必須要有 `train` 和 `validation` 子目錄。
       - 在每一個子目錄內，必須要有您的分類目錄。
  2. 將影像大小標準化，然後設定子目錄，以用於訓練和驗證。
  3. 預先處理資料，以重新調整及擷取影像和其類別。
  4. 定義並訓練模型。
  5. 儲存模型。
  6. 部署模型。

7. 指派 `APIClient`，訂閱資產，並對模型評分，以便配置 {{site.data.keyword.aios_short}}。
8. 配置可解釋性。
   9. 啟用可解釋性。
   10. 取得交易的解釋。
   11. 顯示所解釋的影像。 

## 解釋影像模型的交易
{: #ie-image-workingviewing}

對於可解釋性的影像分類模型範例，您可以看到影像中，哪些部分會正面造成所預測的輸出結果，哪些部分會負面造成所預測的輸出結果。在下列範例中，正面窗格中的影像顯示對預測造成正面影響的部分，負面窗格中的影像顯示對輸出結果造成負面影響的影像部分。

![顯示可解釋性影像分類信賴度明細，其中提供狗的影像，此外還提供強調顯示圖片中的某些部分，以顯示影像中的哪一部分有助於決定該影像是一隻狗](images/insight-explain-image.png)

對於 {{site.data.keyword.pm_full}}，要傳送進行有效負載記載之影像分類模型的評分輸入，不能超過 ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMB。若要避免發生逾時問題，影像不得超過 125 x 125 像素，且必須循序傳送，如此才會在第一個影像完成時，要求取得第二個影像的解釋。
{: note}


## 影像模型範例
{: #ie-image-working-ntbks}

請使用下列兩個記事本，查看詳細的程式碼範例，並開發您自己的 {{site.data.keyword.aios_short}} 部署：

- [指導教學：產生影像型模型的解釋](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [指導教學：產生影像型二元分類器模型的解釋](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

