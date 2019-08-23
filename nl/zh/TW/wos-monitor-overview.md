---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: deployment, monitors, data

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

# 準備適用於部署的監視器
{: #mo-config}

針對您要使用 {{site.data.keyword.aios_short}} 來追蹤的每一項部署，設置並啟用監視器。
{: shortdesc}

例如，在互動式指導教學中，如果您使用 **German Credit Risk 模型**，請選取模型部署，設定有效負載記載的資料類型，並確認模型明細區段所隨附的一些設定。

## 選取部署
{: #mo-select-deploy}

1. 從**洞察**標籤，按一下**新增至儀表板**按鈕。 

   會出現可用的模型部署清單。如果您看不到任何模型部署，則必須使用機器學習提供者來部署模型。在本指導教學中，請選取 **German Credit Risk 模型**。

   ![會顯示「選取模型部署」畫面。其中顯示所選取的機器學習提供者和部署。](images/wos-select-model-deployment.png)

2. 按一下模型部署，然後按一下**配置**。

   如果給定模型有多項部署，當您配置其中一項部署時，同一模型的其他所有部署也會跟著配置。

   儲存您的選擇之後，即可準備配置監視器，包括有效負載記載、精確度和公平性。 

2. 如果要開始，請按一下**配置監視器**。

## 提供有效負載記載的明細
{: #mo-work-data}

您必須提供您模型和訓練資料的相關資訊。如需訓練資料的相關資訊，請參閱[為何 {{site.data.keyword.aios_short}} 需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    就本指導教學來說，請在**資料類型**欄位中，選取**數值/種類**，並針對**演算法類型**，選取**二進位分類**。

![會顯示「指定輸入的類型」畫面，其中顯示所選取的資料類型和演算法類型](images/config-what-monitor.png)

- 如果您所用 {{site.data.keyword.pm_full}} 實例的所在地區，與您的 {{site.data.keyword.aios_short}} 實例相同，您必須選取「資料類型」和「演算法類型」，不過，會為您自動配置有效負載記載資訊。 
- 否則，必須在**有效負載記載**標籤和視窗中，輸入您資料類型、演算法類型和有效負載記載的相關資訊。 

   視您的選擇而定，會有特定的需求。如需相關資訊，請參閱[數值/種類資料](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan)。

   您需要先複製其中一個要執行的程式碼 Snippet，才能配置監視器。請在您的用戶端應用程式中執行 cURL 指令，或在資料科學記事本中執行 Python 指令。這可讓您藉以記載模型部署要求，並將回應資料寫入至有效負載資料庫。
   
在您使用本端 {{site.data.keyword.pm_full}} 方法或使用 API，來傳送有效負載記載明細之後，必須回到**有效負載記載**畫面，並按一下**我已完成**。

![此圖顯示「有效負載記載」畫面](images/payload-logging-gosales001.png)

如果已正確將評分傳送給 {{site.data.keyword.aios_short}}，在您按一下**我已完成**按鈕之後，會顯示下列畫面。會隱藏按鈕，您會看到**已順利啟動記載**訊息。

![順利上傳資料之後的有效負載記載畫面圖](images/payload-logging-gosales002.png)


### 提供模型明細
{: #mo-work-model-dets}

提供您模型的相關資訊，讓 {{site.data.keyword.aios_short}} 可以存取資料庫，並瞭解模型的設置方式。例如，在互動式指導教學中，如果您使用 **German Credit Risk 模型**，則會為您自動完成下列許多欄位。

特別是如果要配置監視器，您必須執行下列作業：

1. 指定訓練資料的位置。做法是輸入位置、主機名稱或 IP 位址、資料庫名稱，以及鑑別資訊。
2. 在資料庫內，您必須選取綱目和表格，以選取訓練表格。
3. 從訓練表格中選取標籤直欄，例如，在本指導教學中，請按一下**風險**圖磚。
4. 選取用來訓練 AI 部署的特性。
5. 選取文字及種類特性。
6. 選取部署預測直欄，例如，在本指導教學中，按一下 **predictedLabel**圖磚。
7. 最後，您可以先檢閱模型明細，再加以儲存。

下列各節根據模型的類型，提供您會遇到的特定資訊：[數值/種類資料](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan)或[影像和非結構化文字](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datai)。


### 數值/種類資料
{: #mo-nuca}

對於數值或種類資料，您需要提供模型訓練資料的相關資訊，才能配置監視器。

- **手動配置監視器** - 您必須提供訓練資料的連線資訊。

    - 選取[演算法類型](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)，並按**下一步**：

      訓練資料的格式必須符合模型。例如，如果模型預期 `Gender` 特性應為 `M` 和 `F`，則訓練資料應具有 `M` 和 `F`，而非 `Male` 和 `Female`。{{site.data.keyword.aios_short}} 現行版本僅支援 Db2 資料庫或 Cloud Object Storage 的位置。{: important}

    - 指定位置（`Db2` 或 `Cloud Object Storage`），然後：

        - 若為 Db2 資料庫，請輸入下列資訊：

            - 主機名稱或 IP 位址
            - 埠
            - 資料庫（名稱）
            - 使用者名稱
            - 密碼

        - 若為 Cloud Object Storage，請輸入下列資訊：

            - 登入 URL：「登入 URL」必須符合您訓練資料所在儲存區的地區設定。您將在下一步中指定訓練資料的儲存區。
            - 資源實例 (ID)
            - API 金鑰

    - 為了確定連線是有效的，請按一下**測試**按鈕，來連接至訓練資料。
    - 指定訓練資料在 Db2 資料庫或 Cloud Object Storage 中的確切位置。

        - 若為 Db2 資料庫，請同時選取含有您模型預期之直欄的綱目和訓練表格。
        - 若為 Cloud Object Storage，請選取一個「儲存區」和「資料集」。

- **上傳配置檔** - 如果您偏好讓訓練資料維持專用，請選擇這個選項。您可以使用自訂 Python 記事本，以提供資訊給 {{site.data.keyword.aios_short}} 來分析您的訓練資料，而不提供對訓練資料本身的存取權。

  執行 Python 記事本，可讓您擷取綱目直欄中的特殊值，以及擷取直欄名稱。此外，您可以使用記事本來預先配置「公平性」監視器。

   - 下載[自訂記事本](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external}，並以您自己的認證取代任何認證。
   - 仔細檢閱記事本，並在適當情況下，指定模型的資料。儲存記事本。
   - 執行記事本，以產生 JSON 格式的配置檔。
   - 上傳 JSON 配置檔。

     ![上傳配置 JSON](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} 會從隨模型一起儲存在 {{site.data.keyword.pm_full}} 中的 meta 資料，找出您的訓練資料。請從訓練資料中選擇含有預測值的標籤直欄。
- 選取用來訓練模型的直欄 - 這些是您的模型部署預期應存在於要求中的特性。
- 最後，選取含有文字且已轉換成整數的直欄。例如，如果原始訓練資料在 `Gender` 方面含有 `Male` 和 `Female`，且它們現在已分別對映至 `0` 和 `1`，則現在訓練資料在 `Gender` 直欄方面，包含 `0` 和 `1` 值。請識別這類現在包含整數但原本卻是包含文字值的直欄。

### 影像和非結構化文字
{: #mo-imun}

- **影像**

  如果模型可接受影像作為輸入，則影像需要以（高度）x（寬度）x（# 個通道）格式表示，其中每一個點各代表每一個像素的單色或 RGB 值。

- **非結構化文字**

   如果模型可接受文字作為輸入，則會預期模型會接受整個文字，而非以向量表示的文字。

## 檢閱並儲存配置
{: #mo-save}

檢閱您的選擇摘要，並按一下**儲存**以繼續。

  ![選取資料表格](images/config-summary-monitor.png)

### 後續步驟
{: #mo-next}

如果要繼續配置監視器，請按一下**品質**標籤，並按一下**開始**。如需相關資訊，請參閱[配置「品質」監視器](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。
