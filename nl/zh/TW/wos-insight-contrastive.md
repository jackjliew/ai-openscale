---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 對比解釋會使用相關正數和相關負數
{: #ie-pp-pn}

對於對比解釋，{{site.data.keyword.aios_short}} 會顯示相關正數值和相關負數值。
{: shortdesc}

- 相關正數是指發現項，對於判斷「那是什麼」來說很重要。
- 相關負數是指未發現項，且因少了它們而顯得重要。

{{site.data.keyword.aios_short}} 一律會顯示相關正數，不過，有時並無相關負數可顯示。在此情況下，可能是這些特性的值已位於中位數，或者因值已離開中位數，使得預測並無變更。

為了更能充分瞭解，我們假設當 {{site.data.keyword.aios_short}} 計算相關負數值時，它會變更離開其中位數值之所有特性的值。對於相關負數，這指的是離中位數最遠的特性值。如果資料點的值已位於中位數，或者即使變更離開中位數的值之後，預測並無變更，則沒有相關負數可顯示。在相關正數方面，{{site.data.keyword.aios_short}}
會尋找接近中位數之特性值中的最大變更，以致於預測沒有變更。實際上，這表示幾乎一律都有一個相關正數來解釋交易。

