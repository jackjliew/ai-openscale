---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: feedback data, data, feedback, models

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

# 在 {{site.data.keyword.aios_short}} 中將回饋資料格式化及上傳
{: #fmt-upld-fdbk-data}

回饋資料是維護無偏誤模型時不可或缺的。您必須定期將回饋資料上傳至 {{site.data.keyword.aios_full}} 服務，以確保您的模型採用的是保持最新的資料（在您預測應用程式的環境定義中，該資料可能指出一些變更）。藉由回饋迴圈，系統會監視預測的成效，並在必要時重新訓練，以便持續學習。監視及使用產生的回饋，可說是機器學習的核心。下列資訊旨在協助您將回饋資料格式化並且上傳。
(: shortdesc)

## 將回饋資料格式化
{: #fmt-upld-fdbk-data-fmt}

為了能適當讀取回饋資料，必須適當地將它格式化。{{site.data.keyword.aios_short}} 服務接受下列格式：

- CSV 檔案格式，可利用使用者介面或 REST API 上傳
- JSON 檔案格式，只能利用 REST API 上傳

這些檔案格式由 `training_data_schema` 綱目所定義，該綱目提供於訂閱明細中。如果要檢視 `training_data_schema`，請使用 Python API 執行下列指令：

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

如果要將訓練資料綱目與回饋綱目相互比較，您也可以檢視回饋綱目。如果要檢視回饋綱目，請使用 Python API 執行下列指令：

```
subscription.feedback_logging.print_table_schema()
```


### CSV 格式
{: #fmt-upld-fdbk-data-fmt-csv}

對於 CSV 檔案，您通常是以一列直欄名稱，在直欄和列中提供資料。

一般而言，當直欄名稱都是大寫時，不需要引號；對於 Db2，會將它們視為不區分大小寫，不過，對於其他資料庫以及在直欄名稱大小寫混合的實例中，就必須符合大小寫。如果檔案含有直欄名稱，這些直欄不一定要符合表格順序，不過，如果檔案沒有直欄名稱，就必須符合表格順序。可能會出現一些不在原始訓練資料中的直欄。在處理期間會忽略這些直欄。


### JSON 格式
{: #fmt-upld-fdbk-data-fmt-json}

JSON 格式由物件集合組成，且其中的欄位對應至直欄名稱。

