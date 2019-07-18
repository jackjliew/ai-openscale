---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 解釋交易
{: #ie-ov}

對於每一項部署，您可以查看特定交易的可解釋性資料。
{: shortdesc}

## 解釋交易
{: #ie-view}

在選取的部署圖磚中，選取導覽器中的**解釋交易**標籤 (![「解釋交易」標籤](images/insight-transact-tab.png))，並輸入交易 ID。

每當將資料傳送給模型進行評分時，它會在 HTTP 標頭中設定 `X-Global-Transaction-Id` 欄位，以設定一個交易 ID。此交易 ID 會儲存在有效負載表格中。如果要尋找模型之特定評分行為的解釋，請指定該評分要求的相關聯交易 ID。請注意，此行為僅適用於 {{site.data.keyword.pm_full}} 交易，而不適用於非 WML 交易。
{: note}

### 在 {{site.data.keyword.aios_short}} 中尋找交易 ID
{: #ie-find}

1.  從部署的時間圖表中，在圖表內滑動標記，並按一下**檢視明細**鏈結，以便[將特定小時的資料視覺化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。
1.  按一下**檢視交易**按鈕，以[檢視交易 ID 清單](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)。
1.  從清單中，複製其中一個交易 ID，並貼到**解釋交易**頁面上的搜尋方框，然後按 Enter 鍵。

    交易 ID 清單也會提供選項，您只需在任何交易 ID 的「動作」直欄中，按一下**解釋**鏈結，如此即會在「可解釋性」標籤中開啟該交易。
    {: note}

  請參閱下列各節，取得各種不同模型類型的解釋範例。

  ![可解釋性交易 ID](images/insight-explain-trans-id.png)

## 種類模型範例
{: #ie-class}

這個可解釋性範例指的是一個二進位分類模型，用來核准或拒絕保險理賠。在本例中，您可以看到正面或負面造成 `DENIED` 最終輸出結果的一些因素。

值為 `< 1 year` 的*原則歷時*特性在決定了 DENIED 輸出結果的模型中，所造成的影響最大。造成此輸出結果的其他特性還有*理賠頻率* (`High`) 和*年齡* (`18`)，以及僅帶來些微影響的*汽車價格* (`$50,000`)。

![可解釋性的二進位分類](images/insight-explain-binary.png)

儘管在決定交易的輸出結果時，圖表有助於顯示最重要的因素，分類模型也可以包含進階解釋，且這些解釋詳述於 `Minimum changes for Approved outcome` 和 `Minimum changes for this outcome` 區段中。

進階解釋不適用於迴歸、影像和非結構化文字模型。
{: note}

`Minimum changes for Approved outcome` 指出，如果特性的值已變更為此區段所列出的值，則模型的預測將會變更。

同樣地，`Minimum changes for this outcome` 指出，即使特性的值已變更為此區段所列出值，模型的預測並未變更。

因此由這兩個值可看出，模型在要產生解釋之資料點附近的行為。

![可解釋性的二進位分類](images/insight-explain-binary2.png)

## 影像模型
{: #ie-image}

{{site.data.keyword.aios_short}} 支援影像資料的可解釋性。

### 使用影像模型
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

### 解釋影像模型的交易
{: #ie-image-workingviewing}

對於可解釋性的影像分類模型範例，您可以看到影像中，哪些部分會正面造成所預測的輸出結果，哪些部分會負面造成所預測的輸出結果。在下列範例中，正面窗格中的影像顯示對預測造成正面影響的部分，負面窗格中的影像顯示對輸出結果造成負面影響的影像部分。

![可解釋性的影像分類](images/insight-explain-image.png)

對於 {{site.data.keyword.pm_full}}，要傳送進行有效負載記載之影像分類模型的評分輸入，不能超過 1 MB。若要避免發生逾時問題，影像不得超過 125 x 125 像素，且必須循序傳送，如此才會在第一個影像完成時，要求取得第二個影像的解釋。
{: note}


### 影像模型範例
{: #ie-image-working-ntbks}

請使用下列兩個記事本，查看詳細的程式碼範例，並開發您自己的 {{site.data.keyword.aios_short}} 部署：

- [指導教學：產生影像型模型的解釋](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [指導教學：產生影像型二元分類器模型的解釋](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## 非結構化文字模型
{: #ie-unstruct}

{{site.data.keyword.aios_short}} 支援非結構化文字資料的可解釋性。

### 使用非結構化文字模型
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

### 解釋非結構化文字的交易
{: #ie-unstruct-xplan}

下列的可解釋性範例顯示用來評估非結構化文字的分類模型。解釋顯示對模型預測造成正面及負面影響的關鍵字。我們也會針對原始文字中被當成輸入輸送給模型的識別關鍵字，顯示其位置。

![可解釋性的影像分類](images/insight-explain-text.png)

### 非結構化文字模型範例
{: #ie-unstruct-ntbkssample}

請使用下列記事本，查看詳細的程式碼範例，並開發您自己的 {{site.data.keyword.aios_short}} 部署：

- [指導教學：產生文字型模型的說明](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

## 對比解釋使用相關正數和相關負數
{: #ie-pp-pn}

對於對比解釋，{{site.data.keyword.aios_short}} 會顯示相關正數值和相關負數值。 

- 相關正數是指發現項，對於判斷「那是什麼」來說很重要。
- 相關負數是指未發現項，且因少了它們而顯得重要。

{{site.data.keyword.aios_short}} 一律會顯示相關正數，不過，有時並無相關負數可顯示。在此情況下，可能是這些特性的值已位於中位數，或者因值已離開中位數，使得預測並無變更。

為了更能充分瞭解，我們假設當 {{site.data.keyword.aios_short}} 計算相關負數值時，它會變更離開其中位數值之所有特性的值。對於相關負數，這指的是離中位數最遠的特性值。如果資料點的值已位於中位數，或者即使變更離開中位數的值之後，預測並無變更，則沒有相關負數可顯示。在相關正數方面，{{site.data.keyword.aios_short}}
會尋找接近中位數之特性值中的最大變更，以致於預測沒有變更。實際上，這表示幾乎一律都有一個相關正數來解釋交易。

