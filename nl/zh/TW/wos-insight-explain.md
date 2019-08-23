---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 解釋交易
{: #ie-ov}

對於每一項部署，您可以查看特定交易的可解釋性資料。只有在具備下列條件，交易才會出現：有資料支援監視器並以您設定的臨界值為基礎、排定監視器執行的時間、{{site.data.keyword.pm_full}} 可提供有效負載資料。
{: shortdesc}

## 依交易 ID 來檢視解釋
{: #ie-view}

1. 按一下部署圖磚。
2. 按一下導覽器中的**解釋交易**標籤 ( ![「解釋交易」標籤](images/insight-transact-tab.png) )。
3. 輸入交易 ID。

每當將資料傳送給模型進行評分時，它會在 HTTP 標頭中設定 `X-Global-Transaction-Id` 欄位，以設定一個交易 ID。此交易 ID 會儲存在有效負載表格中。如果要尋找模型之特定評分行為的解釋，請指定該評分要求的相關聯交易 ID。請注意，此行為僅適用於 {{site.data.keyword.pm_full}} 交易，而不適用於非 WML 交易。
{: note}

## 在 {{site.data.keyword.aios_short}} 中尋找交易 ID
{: #ie-find}

1.  從部署的時間圖表中，在圖表內滑動標記，並按一下**檢視明細**鏈結，以便[將特定小時的資料視覺化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。
1.  按一下**檢視交易**按鈕，以[檢視交易 ID 清單](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)。
1.  從清單中，複製其中一個交易 ID，並貼到**解釋交易**頁面上的搜尋方框，然後按 Enter 鍵。

    交易 ID 清單也會提供選項，您只需在任何交易 ID 的「動作」直欄中，按一下**解釋**鏈結，如此即會在「可解釋性」標籤中開啟該交易。
    {: note}

  請參閱下列各節，取得各種不同模型類型的解釋範例。

  ![可解釋性交易 ID](images/insight-explain-trans-id.png)

## 透過圖表明細來尋找解釋
{: #ie-view-ui}

由於公平性和漂移度量都有解釋，您可以按一下圖表，取得資料集的詳細視圖，然後針對公平性度量，按一下**檢視交易**按鈕，或是按一下漂移交易圖磚，以查看交易的解釋。

- 針對其中一個公平性屬性（例如：性別或年齡），按一下該屬性，按一下圖表，然後按一下**檢視交易**按鈕。
- 若為漂移監視器，請按一下**漂移幅度**，按一下圖表，然後按一下圖磚，以查看與該特定漂移群組相關聯的交易。

## 後續步驟
{: #ie-trans-id-next}

- [解釋種類模型](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [解釋影像模型](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [解釋非結構化文字模型](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [對比解釋](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
