---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 自訂機器學習引擎
{: #fmrk-workaround-customengine}

自訂機器學習引擎可提供機器學習模型和 Web 應用程式的基礎架構和代管功能。{{site.data.keyword.aios_short}} 支援的自訂機器學習引擎必須符合下列需求：

- 顯現兩種類型的 REST API 端點：

   * 探索端點（GET 部署和明細清單）
   * 評分端點（線上和即時評分）

- 所有端點都需要相容於所要支援的 Swagger 規格。

- 與部署之間往來的輸入有效負載和輸出必須符合規格中說明的 JSON 檔案格式。

在這個階段，只支援 `BasicAuth` 或 `none` 格式。
{: Note}

下列範例顯示 REST API 端點規格：

![Swagger 文件中顯示的 REST API 端點規格](images/wosdeployments.png)


下列範例顯示輸入有效負載的格式：

![顯示輸入有效負載範例](images/wosinputdata.png)


## 自訂機器學習引擎何時會是最佳選擇？
{: #fmrk-workaround-enging-choice}

若為下列情況，則自訂機器學習引擎會是最佳選擇：

- 您並沒有使用任何可用的現成產品，來處理您的機器學習模型。您才剛開發了自己的系統來處理這件事。對此，{{site.data.keyword.aios_short}} 不提供直接支援，未來也不會。
- {{site.data.keyword.aios_short}} 尚不支援您用來處理模型的協力廠商引擎。在此情況下，請考量開發一個自訂機器學習引擎，以作為您原始或原生部署的封套。

## 後續步驟
{: #fmrk-workaround-nxt-steps-over}

使用這些[自訂機器學習範例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)之一，來實作您自己的解決方案。
