---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: machine learning, services, ml, custom 

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

# 指定「自訂」ML 服務實例
{: #co-connect}

您在 {{site.data.keyword.aios_short}} 工具中的首要步驟是指定一個服務實例。您的服務實例就是您儲存 AI 模型和部署的所在。
{: shortdesc}

## 連接您的「自訂」服務實例
{: #co-config}

{{site.data.keyword.aios_short}} 會連接至服務實例中的 AI 模型和部署。

1.  從 {{site.data.keyword.aios_short}} 工具首頁，按一下**開始**。

    ![首頁](images/gs-config-start.png)

2.  選取**自訂**圖磚，並按**下一步**。

    ![選取「自訂」](images/connect-custom.png)

3.  選取下列其中一個選項，以連接至部署：

    ![選取「自訂」](images/connect-custom-deploy.png)

4.  如果您選取「輸入個別的評分端點」圖磚，請輸入您的認證：

    ![輸入服務認證](images/connect-custom-cred.png)

5.  按**下一步**。

    - 如果您選取「輸入個別的評分端點」圖磚，您必須提供部署名稱和端點：

      ![輸入服務認證](images/connect-custom-endpoint.png)

      按**下一步**。

    - 如果您選取「要求部署清單」圖磚，您必須提供主機名稱（或 IP 位址）和埠號：

      ![輸入服務認證](images/connect-custom-apiendpoint.png)

      按**下一步**。

      然後從部署清單中選取：

      ![輸入服務認證](images/connect-custom-apiendpoint2.png)

6.  檢閱您選取的部署。

    ![輸入服務認證](images/connect-custom-deploy2.png)

7.  按**下一步**。

### 如何運作
{: #co-works}

這個影像顯示「自訂」環境支援：

![「自訂」如何運作](images/custom-how-works.png)

您也可以參考下列鏈結：

[AIOS 有效負載記載 API![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[自訂部署 API![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python 用戶端連結 SDK![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[使用「自訂」機器學習引擎![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  上述評分輸出應可從作用中的評分端點來存取，而 {{site.data.keyword.aios_short}} 可透過 REST 來呼叫該端點。若為 AzureML、SageMaker 和 WML，{{site.data.keyword.aios_short}} 會直接連接至原生評分端點（因此您不用擔心評分規格的實作）

### 後續步驟
{: #co-next}

{{site.data.keyword.aios_short}} 現在已備妥可供您[指定資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)。
