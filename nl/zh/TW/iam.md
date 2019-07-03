---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


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

下表詳述對映至平台管理角色的動作。平台管理角色可讓使用者在平台層次對服務資源執行作業，例如，將服務的存取權指派給使用者，建立或刪除實例，以及將實例連結至應用程式。

|平台管理角色|動作說明|範例動作|
|--------------------------|------------------------|-----------------------------------------------------------------|
|檢視者|說明| <ul><li>範例 1</li><li>範例 2</li></ul>                   |
|編輯者|說明|<ul><li>範例 1</li><li>範例 2</li></ul>                    |
|操作員|說明| <ul><li>範例 1</li><li>範例 2</li><li>範例 3</li></ul> |
|管理者|說明|<ul><li>範例 1</li><li>範例 2</li><li>範例 3</li></ul>  |
{: caption="表 1. IAM 使用者角色和動作" caption-side="top"}


下表詳述對映至服務存取角色的動作。服務存取角色可讓使用者存取 {{site.data.keyword.aios_short}} 以及可以呼叫 {{site.data.keyword.aios_short}} API。

|服務存取角色|動作說明|範例動作|
|---------------------|------------------------|-----------------------------------------------------------------|
|讀者|說明| <ul><li>範例 1</li><li>範例 2</li></ul>                   |
|撰寫者|說明|<ul><li>範例 1</li><li>範例 2</li></ul>                    |
|管理員|說明| <ul><li>範例 1</li><li>範例 2</li><li>範例 3</li></ul> |
{: caption="表 2. IAM 服務存取角色和動作" caption-side="top"}


如需在使用者介面中指派使用者角色的相關資訊，請參閱[管理對資源的存取權](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)。

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
