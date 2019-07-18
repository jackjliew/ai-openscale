---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# 指定「自訂」ML 服務實例
{: #co-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個服務實例。您的服務實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

## 連接您的「自訂」服務實例
{: #co-config}

{{site.data.keyword.aios_short}} 會連接至服務實例中的 AI 模型和部署。您可以連接自訂服務

1. 從**配置**標籤，按一下**機器學習提供者**。

   ![會顯示選取您的機器學習服務提供者畫面，其中含有支援的機器學習引擎圖磚](images/wos-machine-learning-providers-selection.png)

2. 選取**自訂環境**圖磚。

   ![選取「自訂」](images/ml-custom-provider.png)

3. 輸入您自訂機器學習提供者的名稱和說明，並按**下一步**。 

4. [要求取得清單](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list)或[輸入個別的評分端點](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints)，以選擇是否連接至您的部署。

   ![選取「自訂」](images/ml-custom-connect-deployments.png)
    
5. 按**下一步**。

### 要求取得部署清單
{: #co-config-request-list}

1. 如果您選取**要求取得部署清單**圖磚，請輸入您的認證和 API 端點，然後按一下**儲存**。

   ![輸入服務認證](images/connect-custom-cred.png)

2. 儲存您的機器學習設置之後，請回到**儀表板**，按一下**洞察**標籤，然後按一下**新增部署**按鈕。

3. 從清單中選取部署，並按一下**配置**。

現在，您可準備配置監視器。

### 提供個別的評分端點
{: #co-config-scoring-endpoints}

1. 如果您選取**輸入個別的評分端點**圖磚，請輸入您的 API 端點認證，然後按一下**儲存**。

2. 儲存您的機器學習設置之後，請回到**儀表板**，按一下**洞察**標籤，然後按一下**新增部署**按鈕。

3. 按一下**新增端點**按鈕。

4. 從下拉功能表中，選取自訂環境，輸入部署名稱和 API 端點，然後按一下**儲存**。

現在，您可準備配置監視器。

### 如何運作
{: #co-works}

下列影像顯示「自訂」環境支援：

![「自訂」如何運作](images/custom-how-works.png)

您也可以參考下列鏈結：

[{{site.data.keyword.aios_short}} 有效負載記載 API](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[自訂部署 API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python 用戶端連結 SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[使用自訂機器學習引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python SDK for IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **支援監視器的模型輸入準則**

  您的模型應以特性向量作為輸入，這其實就是具名欄位和其值的集合（要監視其偏誤的欄位，就會成為這其中一個欄位）：

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  在本例中，`"age"` 可能就是某人要評估其公平性的欄位。

  如果輸入是一個張量/矩陣，而從輸入特性空間轉換而來（若是從文字或影像深度學習，往往就是如此），在現行版本中，{{site.data.keyword.aios_short}} 平台無法處理該模型。乃至於，如果深度學習模型含有文字或影像輸入，就無法處理以進行偏誤的偵測和減輕。

  此外，應載入訓練資料，以支援「可解釋性」。

  對於文字的可解釋性，完整文字應為其中一項特性。在現行版本中，若為「自訂」模型，則不支援影像的可解釋性。
  {: note}

- **支援監視器的模型輸出準則**

  除了您模型中各種類別的預測機率，該模型也應該輸出輸入特性向量。

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  在本例中，`"personal"` 和 `"camping"` 是可能的類別，每一個評分輸出中的評分都會指派給這兩個類別。如果遺漏預測機率，偏誤偵測將會運作，但自動除去偏誤不會運作。

  上述評分輸出應可從作用中的評分端點來存取，而 {{site.data.keyword.aios_short}} 可透過 REST 來呼叫該端點。若為 AzureML、SageMaker 和 {{site.data.keyword.pm_full}}，{{site.data.keyword.aios_short}} 會直接連接至原生評分端點（因此您不用擔心評分規格的實作）。

### 後續步驟
{: #co-next}

{{site.data.keyword.aios_short}} 現在已備妥，可供您[配置監視器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
