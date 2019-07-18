---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# 高可用性和災難回復
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} 具備高可用性，可位於多個 {{site.data.keyword.cloud_notm}} 位置（例如：達拉斯和華盛頓特區）內。不過，如果要從足以影響整個位置的潛在災難回復，則需要做好規劃及準備。
{: shortdesc}

您負責瞭解服務的配置、自訂和使用情形。您也要負責做好準備以便將服務的實例重建在新位置，以及還原您在任何位置的資料。請參閱[如何確保零停機？](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external}，以取得相關資訊。

## 高可用性 
{: #openscale-high-availability}

透過在三個可用區域上採取多重區域遞送方式 (MZR)，{{site.data.keyword.aios_short}} 已部署及提供於**美國南部**的資料中心上。不論何時，只要有一個區域無法使用，仍可在其他的可用性區域中繼續使用該系統。廣域負載平衡器和 DNS 伺服器會將資料流量遞送至可用的區域，完全不會岔斷使用者。

儲存在 PostgreSQL 資料庫中的資料也具備高可用性，並且存在於多個可用性區域中。不過，客戶需負責備份資料以支援災難回復計劃，如此才能重建服務。

{{site.data.keyword.aios_short}} 資料流量分散在一個地區的多個區域中。在相同地區中，每一個區域就是一個資料中心。 

Compose 資料庫（例如：PostgreSQL 和分散式 <code>etc</code> 目錄 (etcd) 資料庫）會定期備份，以確保高可用性，萬一出現災難，{{site.data.keyword.aios_short}} 作業團隊就能夠在「回復點目標 (RPO)」內回復服務。
 
{{site.data.keyword.cloud_notm}} 提供地區內的資料備援，藉以提供高可用性保護。對於含有訓練及/或自訂模型資料的用戶端資料庫，IBM 提供自動資料抄寫，不需額外付出任何成本。會在 {{site.data.keyword.cloud_notm}} 資料中心內，於該地區內的各個可用性區域之間完成抄寫。
 
## 備份及還原
{: #openscale-restore}

用戶端需負責備份及還原其自己的資料，包括訓練及/或自訂模型資料，以及用戶端產生的任何自訂模型。如需用戶端備份及還原指示，請參閱 {{site.data.keyword.cloud_notm}} 說明文件。
 
## 災難回復
{: #openscale-disaster-recovery}

藉由在 {{site.data.keyword.cloud_notm}} 資料中心內，於該地區中的各個可用性區域之間進行自動抄寫，可達成「地區內的業務持續」。用戶端需負責多地區的災難回復。這些責任包括：備份、還原及同步化自己的安全原則、訓練及/或自訂模型資料，以及用戶端產生的任何自訂模型。此外，用戶端還需負責遞送及/或平衡各地區之間的負載。如需用戶端備份及還原指示，請參閱 {{site.data.keyword.cloud_notm}} 說明文件。
