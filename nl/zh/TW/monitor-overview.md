---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: deployment, monitors, data

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 準備適用於部署的監視器
{: #mo-config}

針對您要使用 {{site.data.keyword.aios_short}} 來追蹤的每一項部署，設置並啟用監視器。
{: shortdesc}

## 選取部署
{: #mo-select-deploy}

1.  首先，您必須選取一項部署。

    如果給定模型有多項部署，當您配置其中一項部署時，同一模型的其他所有部署也會跟著配置。{: note}

    ![「選取部署」頁面](images/config-select-deploy.png)

1.  選取*準備監視*圖磚。

    ![準備監視](images/config-prep-monitor.png)

## 使用資料
{: #mo-work-data}

1.  現在，您將提供模型及訓練資料的相關資訊；請按**下一步**。如需訓練資料的相關資訊，請參閱 [{{site.data.keyword.aios_short}} 為何需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

    ![準備解釋](images/config-what-monitor.png)

1.  從下拉功能表中，選取您部署要分析的資料類型，然後按**下一步**。

    ![選取輸入類型](images/config-input-monitor.png)

### 數值/種類資料
{: #mo-nuca}

對於數值或種類資料，您需要提供模型訓練資料的相關資訊，才能配置監視器。

  ![選取配置類型](images/config-manual-monitor.png)

- **手動配置監視器** - 您必須提供訓練資料的連線資訊。

    - 選取[演算法類型](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)，並按**下一步**：

      ![多類別](images/multiclass.png)

      請確定訓練資料的格式與您模型預期的格式完全相同。例如，如果模型預期 *Gender* 特性應為 `M` 和 `F`，則訓練資料應具有 `M` 和 `F`，而非 `Male` 和 `Female`。目前 {{site.data.keyword.aios_short}} 只支援 Db2 資料庫或 Cloud Object Storage 位置。{: important}

    - 指定位置（`Db2` 或 `Cloud Object Storage`），然後：

        - 若為 Db2 資料庫，請完成下列項目：

            - 主機名稱或 IP 位址
            - 埠
            - 資料庫（名稱）
            - 使用者名稱
            - 密碼

            ![「指定訓練資料的 Db2 位置」頁面](images/config-train-db2-monitor.png)

        - 若為 Cloud Object Storage，請完成下列項目：

            - 登入 URL

              「登入 URL」必須符合您訓練資料所在儲存區的地區設定。您將在下一步中指定訓練資料的儲存區。{: important}

            - 資源實例 (ID)
            - API 金鑰

            ![「指定訓練資料的 Cloud Object Storage 位置」頁面](images/config-train-cos-monitor.png)

    - 按一下**測試**按鈕來連接至訓練資料，以確定連線是有效的。按**下一步**。

    - 指定訓練資料在 Db2 資料庫或 Cloud Object Storage 中的確切位置。

        - 若為 Db2 資料庫，請同時選取含有您模型預期之直欄的綱目和訓練表格：

          ![指定綱目和訓練表格中的 Db2 位置](images/fair-config-table-db2.png)

        - 若為 Cloud Object Storage，請選取一個「儲存區」和「資料集」：

          ![指定資料集的 Cloud Object Storage 位置](images/fair-config-dset-cos.png)

          按**下一步**，繼續以下的步驟 5。

- **上傳配置檔** - 如果您偏好讓訓練資料維持專用，請選擇這個選項。您可以使用自訂 Python 記事本，以提供資訊給 {{site.data.keyword.aios_short}} 來分析您的訓練資料，而不提供對訓練資料本身的存取權。

  執行 Python 記事本，可讓您擷取綱目直欄中的特殊值，以及擷取直欄名稱。此外，您可以使用記事本來預先配置「公平性」監視器。

    - 下載[自訂記事本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window}，並以您自己的認證取代任何認證。

    - 仔細檢閱記事本，並在適當情況下，指定模型的資料。儲存記事本。

    - 執行記事本，以產生 JSON 格式的配置檔。

    - 上傳 JSON 配置檔。

        ![上傳配置 JSON](images/config-json-monitor.png)

    - 按**下一步**。

- {{site.data.keyword.aios_short}} 會從隨模型一起儲存在 WML 中的 meta 資料，找出您的訓練資料。請從訓練資料中選擇含有預測值的標籤直欄，並按**下一步**。

  ![選取直欄標籤](images/fair-config-column.png)

- 選取用來訓練模型的直欄 - 這些是您的模型部署預期應存在於要求中的特性。按**下一步**。

    ![選取直欄標籤](images/explain-select-column.png)

- 最後，選取含有文字且已轉換成整數的直欄。例如，如果原始訓練資料在 *Gender* 方面含有 `Male` 和 `Female`，且它們現在已分別對映至 `0` 和 `1`，則現在訓練資料在 *Gender* 直欄方面，包含 `0` 和 `1` 值。請識別這類現在包含整數但原本卻是包含文字值的直欄。按**下一步**。

    ![選取資料表格](images/explain-text-column.png)

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

如果要開始配置監視器，請選取一個種類，並按一下**開始**。
