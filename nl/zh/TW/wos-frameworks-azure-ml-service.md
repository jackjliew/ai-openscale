---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Microsoft Azure ML Service 架構
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} 完整支援下列的 Microsoft Azure Machine Learning Service 架構：
{: shortdesc}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|原生|分類|結構化|
|scikit-learn|分類|結構化|
|scikit-learn|迴歸|結構化|
{: caption="架構支援明細" caption-side="top"}

## 將 Microsoft Azure ML Service 新增至 {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

您可以使用下列其中一種方法，將 {{site.data.keyword.aios_short}} 配置成使用 Microsoft Azure ML Service：

- 如果您是第一次將機器學習提供者新增至 {{site.data.keyword.aios_short}}，您可以使用配置介面。如需相關資訊，請參閱[指定 Microsoft Azure ML Service 實例](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)。
- 您也可以使用 Python SDK 來新增機器學習提供者。如果您希望有多個提供者，必須使用此方法。如需透過程式來執行此項的相關資訊，請參閱[連結 Microsoft Azure 機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)。


{{site.data.keyword.aios_short}} 會呼叫與 Azure ML Service 所需的各種不同 REST 端點。如果要這樣做，您必須連結 Azure Machine Learning Service {{site.data.keyword.aios_short}}。

1. 建立一個 Azure Active Directory 服務主體。
2. 在新增 Azure ML Service 服務連結時（不論是透過使用者介面或 Python {{site.data.keyword.aios_short}} SDK），請指定認證詳細資料。

## JSON 要求和回應檔案的需求
{: #frmwrks-azureservice-JSON}

若要讓 {{site.data.keyword.aios_short}} 能使用 Azure ML Service，您所建立的 Web 服務部署必須符合特定需求。根據以下所述的需求，您建立的 Web 服務部署必須接受 JSON 要求，並且傳回 JSON 回應。

### 必要的 Web 服務 JSON 要求格式
{: #frmwrks-azureservice-JSON-sample-request}

- REST API 要求內文必須是 JSON 文件，且含有一個由 JSON 物件組成的 JSON 陣列。
- JSON 陣列的名稱必須是 `"input"`。
- 每一個 JSON 物件只能包含一個簡式鍵值組，其中，值只能是字串、數字、`true`、`false`或 `null`
- 值不能是 JSON 物件或陣列
- 不論是否有非 `null` 值可用，陣列中每一個 JSON 物件所指定的索引鍵（從而索引鍵數目）必須相同


下列範例 JSON 檔案符合上述需求，而可作為用來建立您自己 JSON 要求檔的範本：


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### 必要的 Web 服務 JSON 回應格式
{: #frmwrks-azureservice-JSON-sample-response}

在您建立 JSON 回應檔時，請記下下列項目：

- REST API 回應內文必須是 JSON 文件，且含有一個由 JSON 物件組成的 JSON 陣列。
- JSON 陣列的名稱必須是 `"output"`。
- 每一個 JSON 物件只能包含鍵值組，其中，值只能是字串、數字、`true`、`false`、`null`，或一個不含其他任何 JSON 物件或陣列的陣列。
- 值不能是 JSON 物件
- 不論是否有非 `null` 值可用，陣列中每一個 JSON 物件所指定的索引鍵（以及索引鍵數目）必須相同
- 對於分類模型：Web 服務必須傳回每一個類別的機率陣列，且對於陣列中的每一個 JSON 物件，其機率排序必須一致。
  - 範例：假設您有一個用來預測貸方風險的二進位分類模型，其中的類別是 `Risk` 或 `No Risk`
  - 對於 "output" 陣列中所傳回的每一個結果，物件必須包含鍵值組，內含固定順序的機率，其格式如下：
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

為了與 Azure ML Studio 和 Service 兩者中使用的 Azure ML 視覺化工具一致，建議（但非必要）使用下列的索引鍵名稱：

- 索引鍵名稱 `"Scored Labels"`，用來表示模型預測值的輸出索引鍵
- 索引鍵名稱 `"Scored Probabilities"`，用來表示每一個類別之機率陣列的輸出索引鍵

下列範例 JSON 檔案符合上述需求，而可作為用來建立您自己 JSON 回應檔的範本：


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## 樣本記事本
{: #frmwrks-azureservice-smpl-ntbks}

下列記事本顯示如何使用 Microsoft Azure ML Service：

- [建立資料集區、監視模型部署，以及分析資料](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure Service 模型評分範例](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 進一步探索
{: #frmwrks-azureservice-mediumblogs}

- [AzureMachine Learning 服務與 Studio 有何不同？](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
