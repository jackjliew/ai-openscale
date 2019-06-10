---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

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

# 在 {{site.data.keyword.aios_short}} 中格式化和上载反馈数据
{: #fmt-upld-fdbk-data}

反馈数据对于维护无偏差模型至关重要。必须定期将反馈数据上载到 {{site.data.keyword.aios_full}} 服务，以确保模型将可能指示预测性应用程序上下文中的更改的最新数据考虑在内。借助反馈过程，系统通过监视预测的有效性并在需要时重新训练来持续学习。监视和使用生成的反馈是机器学习的核心所在。以下信息旨在帮助您格式化和上载反馈数据。
(: shortdesc)

## 格式化反馈数据
{: #fmt-upld-fdbk-data-fmt}

要正确读取反馈数据，必须正确将其格式化。{{site.data.keyword.aios_short}} 服务接受以下格式：

- CSV 文件格式，可以通过使用 UI 或 REST API 进行上载
- JSON 文件格式，只能通过使用 REST API 进行上载

这些文件格式由可在预订详细信息中获取的模式 `training_data_schema` 来定义。要查看 `training_data_schema`，请使用 Python API 运行以下命令：

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

要将训练数据模式与反馈模式进行比较，可能也要查看反馈模式。要查看反馈模式，请使用 Python API 运行以下命令：

```
subscription.feedback_logging.print_table_schema()
```


### CSV 格式
{: #fmt-upld-fdbk-data-fmt-csv}

通常对于 CSV 文件而言，您在列和行中提供数据，其中一行表示列名。

通常，在列名全都为大写时无需引号，这使其对于 Db2 而言不区分大小写，但是对于其他数据库以及在列名是大小写混合的情况下，大小写必须匹配。
如果文件包含列名，那么列未必一定与表顺序匹配，但是，如果文件没有任何列名，那么必须与表顺序匹配。可以具有原始训练数据中未包含的列。在处理期间会忽略这些列。


### JSON 格式
{: #fmt-upld-fdbk-data-fmt-json}

JSON 格式由字段与列名对应的对象集合组成。

