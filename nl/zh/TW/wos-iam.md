---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Identity and Access Management 角色和動作

對於您帳戶中的使用者，對 {{site.data.keyword.aios_full}} 服務實例的存取權是由 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 所控制。凡是以您的帳戶來存取 {{site.data.keyword.aios_short}} 服務的每個使用者，都必須賦予一項存取原則，且其中定義了一個 IAM 角色。該原則會決定該使用者在您所選服務或實例的環境定義內，所能執行的動作。{{site.data.keyword.Bluemix_notm}} 服務會將可容許的動作自訂及定義成容許對服務執行的作業。然後，這些動作會對映至 IAM 使用者角色。

原則可讓您在不同層次授與存取權。部分選項包括： 

* 對您帳戶中所有服務實例的存取權
* 對您帳戶中個別服務實例的存取權
* 對實例中特定資源的存取權

定義存取原則的範圍之後，您可以指派一個角色，決定該使用者的存取權層次。請檢閱下列各表，其概述每個角色在 {{site.data.keyword.aios_short}} 服務內所容許的動作。

利用平台管理角色，可以指派各種層次的許可權給使用者，以便在帳戶內以及對服務執行平台動作。例如，針對型錄資源指派的平台管理角色可讓使用者完成建立、刪除、編輯及檢視服務實例等動作。而且，針對帳戶管理服務指派的平台管理角色可讓使用者完成邀請及移除使用者、使用資源群組，以及檢視計費資訊等動作。如需帳戶管理服務的相關資訊，請參閱[指派帳戶管理服務的存取權](/docs/iam?topic=iam-account-services#account-services)。

建立原則時請選取適用的所有角色。每個角色都容許完成不同的動作，而且不會繼承權限較低角色的動作。
{: tip}

下表提供使用者可在型錄資源及資源群組的環境定義內執行的一部分平台管理動作範例。請參閱每個型錄供應項目的文件，以瞭解如何將角色套用至所使用服務之環境定義內的使用者。


|  |一個或所有已啟用 IAM 的服務|在資源群組中選取的服務|選取的資源群組|
|:--------------|:------------|:-------------|:-------------|
|檢視者角色|檢視實例、別名、連結及認證|僅檢視資源群組中指定的實例|檢視資源群組|
|操作員角色|檢視實例，並管理別名、連結及認證|不適用|不適用|
|編輯者角色|建立、刪除、編輯及檢視實例。管理別名、連結及認證|僅建立、刪除、編輯、暫停、回復、檢視及連結資源群組中指定的實例|檢視及編輯資源群組的名稱|
|管理者角色|服務的所有管理動作|資源群組中指定實例的所有管理動作|檢視、編輯及管理資源群組的存取權|
|叢集管理者角色（僅適用於 {{site.data.keyword.wos4d_full}}）|具備 IBM Cloud Private 平台的完整存取權|具備資源群組中之指定實例的完整存取權|以下動作只有叢集管理者才能完成：連接至 LDAP 目錄，新增使用者並指派 IAM 角色給它們，管理所有名稱空間之間的工作量、基礎架構和應用程式，指派配額，新增 Pod 安全原則，新增內部 Helm 儲存庫，刪除內部 Helm 儲存庫，新增 Helm 圖表至內部 Helm 儲存庫，將 Helm 圖表從內部 Helm 儲存庫移除，以及將內部與外部 Helm 儲存庫同步化|
{: row-headers}
{: class="comparison-table"}
{: caption="表 1. 針對帳戶中之服務的範例平台管理角色和動作" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


對於服務存取角色（可讓使用者存取 {{site.data.keyword.aios_short}} 以及能夠呼叫 REST API），{{site.data.keyword.aios_short}} 會因循上述表格中所列出的平台管理角色。如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理對資源的存取權](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。

 
