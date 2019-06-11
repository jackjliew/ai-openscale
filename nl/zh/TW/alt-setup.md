---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Python, install, python module, setup, set up, insights, explainability

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 安裝 Python 模組以設置 {{site.data.keyword.aios_short}}
{: #as-module}

若要自動佈建及配置必要的 {{site.data.keyword.cloud_notm}} 服務，以及查看 {{site.data.keyword.aios_full}} 應用程式（包括樣本資料），您可以安裝 Python 模組。
{: shortdesc}

## 關於此模組
{: #as-about}

- 模組可為技術使用者提供另一種作法，不必自行佈建及配置服務，就可以查看已啟動且正在執行的 {{site.data.keyword.aios_short}} 實例，如[開始使用](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)指導教學所述。
- Python 模組會執行一項程序，以檢查您具有的服務，並且建立必要的服務，包括 {{site.data.keyword.aios_short}}。在模組順利執行之後，您可以從 {{site.data.keyword.cloud_notm}} 儀表板啟動 {{site.data.keyword.aios_short}}，以查看它如何監視模型。

## 開始之前
{: #as-prereqs}

1. [建立 {{site.data.keyword.cloud_notm}}API 金鑰並下載它](/docs/iam?topic=iam-userapikey#create_user_key)。您將需要在後續步驟中輸入 API 金鑰。

2. [安裝 Python 3 任何版本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://www.python.org/downloads/){: new_window}。

  Python 3 含有必要的 pip 套件管理系統。{: note}

3. 執行下列指令，以安裝 `ibm-ai-openscale-cli` 套件：

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    如果您的系統上安裝了多個 pip 版本，您可能需要執行 `pip3` 而非 `pip`，例如 `pip3 install -U ibm-ai-openscale-cli`。
    {: tip}

4. 如果您已有 {{site.data.keyword.pm_short}} 服務實例，請檢查 [{{site.data.keyword.cloud_notm}} 儀表板 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}){: new_window}，以確定該服務是由 {{site.data.keyword.iamshort}} (IAM) 管理，而不是由 Cloud Foundry 管理。

  **重要事項**：模組會檢查是否有 {{site.data.keyword.pm_short}} 實例。如果您有一個實例，模組會使用它。但是如果您的實例是由 Cloud Foundry 所管理，您必須先[將它移轉至 IAM 資源群組，再執行模組](/docs/resources?topic=resources-migrate#migrate)。

## 執行模組
{: #as-run}

請執行下列指令：

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## 在 {{site.data.keyword.aios_short}} 中檢視結果
{: #as-open}

如果要檢視模型之公平性和精確度的相關洞察、受監視資料的明細，以及個別交易的可解釋性，請開啟 [{{site.data.keyword.aios_short}} 儀表板 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}。

- 如果要瞭解樣本資料的實務，請閱讀 [{{site.data.keyword.aios_short}} 的使用案例和值](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use)。

### 檢視洞察
{: #as-insights}

從 [{{site.data.keyword.aios_short}} 儀表板 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}，按一下**洞察**標籤，這會顯示所部署模型的度量概觀：![洞察](images/insight-dash-tab.png)

- 「洞察」頁面會根據所配置的臨界值，顯示公平性和精確度的任何問題，並且一目瞭然。

- 每一項部署各會顯示成一個磚。模組已配置一項稱為 `GermanCreditRiskModel` 的部署，如下列畫面擷取所示：

  ![「洞察」概觀](images/setup01-0206.png)

### 檢視監視資料
{: #as-monitoring}

1. 從「洞察」頁面，按一下 `GermanCreditRiskModel` 圖磚，以檢視受監視資料的相關明細。
2. 在圖表中滑動標記，以檢視某一天和某個時段（這會顯示資料），然後按一下**檢視明細**鏈結。

   - 例如，下列畫面顯示特定日期和時間的資料。日期和時間會因您執行模組的時間而異。

   - 如需解讀時間序列圖表的相關資訊，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale?topic=ai-openscale-it-ov)。

    ![監視資料](images/setup02-0206.png)

3. 如果要查看 `AGE` 資料監視的相關明細，請確定已從下拉功能表中選取 `AGE`。

  - 請注意，在下列畫面擷取中，不存在任何偏誤。

  - 如需解讀某一小時之資料點圖表的相關資訊，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp)。

    ![檢視明細](images/setup03-0206.png)

### 檢視可解釋性
{: #as-explain}

如果要瞭解造成在給定時段出現偏誤的因素，請從前一節所示的視覺化畫面中，選取**檢視交易**按鈕。

會針對存在偏誤的那些交易，列出其過去一小時的交易 ID。對於此模組中使用的模型，可用的要求並無偏誤。因此在下列畫面擷取中，不會顯示該時段的任何交易。

  ![不含任何交易的交易清單](images/setup06-0206.png)

如需尋找及解釋交易的相關資訊，請參閱[解釋交易](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view)。

## 相關資訊
{: #as-info}

- 如果要瞭解偏誤，請參閱[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。
- 如果要瞭解您模型預測輸出結果的精準程度，請參閱[精確度](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。
- 如果要瞭解如何解讀圖表和資料，請參閱[監視「公平性」、「每分鐘的平均要求數」和「精確度」](/docs/services/ai-openscale?topic=ai-openscale-it-ov)。
- 如果要瞭解基礎因素如何影響輸出結果，請參閱[監視可解釋性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。
