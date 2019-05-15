---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

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

# 新增功能
{: #rn-relnotes}

本文件概述 {{site.data.keyword.aios_full_notm}} 的新特性和已知問題。
{: shortdesc}

## 2019 年 3 月 5 日
{: #rn-5March2019}

該服務的新特性和變更如下。

### 新特性和變更
{: #rn-5March2019nf}

從舊版以來已新增或加強的 {{site.data.keyword.aios_short}} 特性包括：

- __*新的 Credit Risk 模型*__：所有的評分引擎都支援新的 Credit Risk 模型範例/指導教學。如需相關資訊，請參閱[開始使用](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted)和[其他資源](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov)主題。

- __*計算除去偏誤*__：您可以在正式作業模型與 {{site.data.keyword.aios_short}} 所建立的除去偏誤模型之間切換。如需相關資訊，請參閱[正式作業模型和除去偏誤模型](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb)以及[瞭解除去偏誤如何運作](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)。

## 2019 年 2 月 22 日
{: #rn-22February2019}

該服務的新特性和變更如下。

### 新特性和變更
{: #rn-22February2019nf}

從舊版以來已新增或加強的 {{site.data.keyword.aios_short}} 特性包括：

- __*使用者介面更新*__：您可以匯入 JSON 檔案，以便在建立訂閱期間，以程式設計方式來配置所有監視器和特性。您也可以匯出配置檔。如需相關資訊，請參閱[使用 JSON 檔案來配置部署訂閱](/docs/services/ai-openscale?topic=ai-openscale-cf-ov)主題。

## 2019 年 2 月 7 日
{: #rn-7February2019}

該服務的新特性和變更如下。

### 新特性和變更
{: #rn-7February2019nf}

從舊版以來已新增或加強的 {{site.data.keyword.aios_short}} 特性包括：

- __*使用者介面更新*__：{{site.data.keyword.aios_short}} 使用者介面已有一些改良，包括[隨需檢查公平性和精確度](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)的作法，以及能夠從[公平性明細圖表](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)來查看交易清單。

- __*「可解釋性」的加強*__：現在所有數字在「相關正向 (PP)」和「相關負向 (PN)」值之間的精準度和小數位數都是相同的。

- __*Db2 SSL 支援*__：{{site.data.keyword.aios_short}} 支援將自簽憑證（Base-64 編碼）與 Db2 認證一起傳遞。

- __*IBM Cloud 資料庫支援*__：除了 Compose for PostgreSQL 和 Db2，{{site.data.keyword.aios_short}} 現在還支援 Databases for PostgreSQL

### 已知問題
{: #rn-7February2019ki}

- **自訂 ML 服務實例**

    - [Python 模組](/docs/services/ai-openscale?topic=ai-openscale-as-module)目前無法將「可解釋性」運用於「自訂」服務實例上。這是因為「自訂」服務實例要求回應資料中需有一項數值預測，但這並未隨附於模組 Script 中。

## 2018 年 12 月 14 日
{: #rn-14December2018}

該服務的新特性、變更和已知問題如下。

### 新特性和變更
{: #rn-12nf}

{{site.data.keyword.aios_short}} 從測試版以來已新增或加強的特性包括：

- __*通用版*__：{{site.data.keyword.aios_full_notm}} 通用版 (GA) 屬於 IBM Cloud 標準（付費）方案。

- __*IBM Cloud Private for Data 1.2 版*__：如果您是在 IBM Cloud Private for Data 1.2 版上使用 {{site.data.keyword.aios_short}}，請參閱這裡的說明文件（包括安裝指示）：[安裝核對清單](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*支援您的模型類型*__：除了 Watson Machine Learning 中的 AI 模型部署，{{site.data.keyword.aios_short}} 還支援 Microsoft Azure、Amazon SageMaker 和「自訂」環境中的模型部署。如需相關資訊，請參閱[支援的模型類型](/docs/services/ai-openscale?topic=ai-openscale-in-ov)。

- __*免費的「精簡」資料庫*__：免費的「精簡」受管理資料庫可提供您在開始使用 {{site.data.keyword.aios_short}} 時所需的一切。如需詳細資料，請參閱 [{{site.data.keyword.aios_short}} 定價方案 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/catalog/services/watson-openscale){: new_window}。

- __*偏誤監視*__：支援 `float` 和 `double` 類型的受保護屬性，以及支援在線性迴歸模型上偵測偏誤。此外，{{site.data.keyword.aios_short}} 可為您自動去除您 AI 模型的偏誤。如需相關資訊，請參閱[瞭解公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

- __*可解釋性*__：支援迴歸模型、Python 函數和補充的對比解釋。如需相關資訊，請參閱[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

- __*資料儲存庫*__：在不倚賴 Watson Machine Learning 情況下進行品質監視，並且能夠使用您自己的資料庫，不論是 Db2、Postgres 或 Db2 on Cloud 都行。

- __*NeuNetS（測試版）*__：IBM Neural Network Synthesizer (NeuNetS) 是以測試版形式提供（限公有雲）。如需相關資訊，請參閱 [NeuNetS 說明文件![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}。

- __*已加強的使用者介面*__：{{site.data.keyword.aios_short}} 使用者介面已改良，而包含直方圖分佈，可讓您從直方圖來切換顯示訓練資料、模型 ID 和版本化，以及交易 ID 表格。如需相關資訊，請參閱[將特定小時的資料視覺化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。

- __*Alternate tutorial set-up option*__：若要自動佈建及配置必要的 IBM Cloud 服務，以及查看 IBM {{site.data.keyword.aios_full}} 應用程式（包括樣本資料），您可以安裝及執行 Python 模組。請參閱[安裝 Python 模組以設置 {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### 已知問題
{: #rn-12ki}

- **Microsoft Azure**

    - Azure Machine Learning Web 服務有兩種類型，但 {{site.data.keyword.aios_short}} 只支援`新`類型。不支援`標準`類型。

    - __*必須使用預設輸入名稱*__：在 Azure Web 服務中，預設輸入名稱是 `"input1"`。目前 {{site.data.keyword.aios_short}} 規定要使用此欄位，如果遺漏，{{site.data.keyword.aios_short}} 就無法運作。

      如果您的 Azure Web 服務不是使用預設名稱，請將輸入欄位名稱變更為 `"input1"`，這樣程式碼就會運作。

- **AWS SageMaker**

    - __*不支援 BlazingText 演算法*__：在 {{site.data.keyword.aios_short}} 現行版本中，不支援 AWS SageMaker BlazingText 演算法輸入承載內容格式。

## 2018 年 9 月 17 日
{: #rn-17September2018}

### 新特性和變更
{: #rn-17nf}

- **測試搶鮮版** - 歡迎使用 {{site.data.keyword.aios_full_notm}} 測試搶鮮版。
