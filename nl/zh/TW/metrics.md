---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 建立自訂監視器和度量 ![測試版標記](images/beta.png)
{: #cst_mtrcs}

自訂監視器會合併一組自訂度量，可讓您以定量方式追蹤模型部署和商業應用程式的任何方面。您可以定義自訂度量，並使用它們來搭配標準度量，例如 {{site.data.keyword.aios_full}} 中所監視的模型品質、效能或公平性度量。
{: shortdesc}

如果要管理自訂監視和度量，您必須使用屬於 Python SDK 一部分的可程式介面。同樣地，您可以在 {{site.data.keyword.aios_short}} 資料集區中儲存自訂度量，以便在需要時加以存取。自訂度量也可以透過視覺化呈現在 {{site.data.keyword.aios_short}} 儀表板上。

## 管理自訂度量
{: #cst_mtrc_mgmt}

若要使用自訂度量，您必須執行下列作業：

1. 在度量定義中登錄自訂監視器。
2. 啟用自訂監視器。
3. 儲存度量值。

下列進階指導教學說明怎麼做：

- [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [使用自訂機器學習引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

您隨時可以停用及啟用自訂監視。如果您不再需要自訂監視器，您可以移除它。

如需相關資訊，請參閱 [Python SDK 文件](http://ai-openscale-python-client.mybluemix.net/)。

## 存取及視覺化自訂度量
{: #cst_mtrcs_viz}

若要存取及視覺化自訂度量，您可以使用可程式介面。下列進階指導教學說明怎麼做：

- [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [使用自訂機器學習引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   如需相關資訊，請參閱 [Python SDK 文件](http://ai-openscale-python-client.mybluemix.net/)。

您自訂度量的視覺化會出現在 {{site.data.keyword.aios_short}} 儀表板上。

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
