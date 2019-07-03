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

## Identity and Access Management 역할 및 조치

계정의 사용자에 대한 {{site.data.keyword.aios_full}} 서비스 인스턴스에 대한 액세스는 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)을 통해 제어됩니다. 계정의 {{site.data.keyword.aios_short}} 서비스에 액세스하는 모든 사용자에게는 IAM 역할이 정의된 액세스 정책을 지정해야 합니다. 정책에 따라 사용자가 선택한 서비스 또는 인스턴스의 컨텍스트 내에서 수행할 수 있는 조치가 결정됩니다. 허용되는 조치는 {{site.data.keyword.Bluemix_notm}} 서비스를 통해 서비스에 대해 수행 가능한 오퍼레이션으로 사용자 정의되고 정의됩니다. 그런 다음 조치가 IAM 사용자 역할에 맵핑됩니다. 

정책을 사용하면 서로 다른 레벨에서 액세스 권한을 부여할 수 있습니다. 몇 가지 옵션은 다음과 같습니다.  

* 계정에서 제공하는 서비스의 모든 인스턴스에 대한 액세스
* 계정에서 제공하는 개별 서비스 인스턴스에 대한 액세스
* 인스턴스 내 특정 리소스에 대한 액세스

액세스 정책의 범위를 정의한 후에는 사용자의 액세스 레벨을 결정하는 역할을 지정하십시오. {{site.data.keyword.aios_short}} 서비스 내에서 각 역할이 허용하는 조치를 설명하는 다음 표를 검토하십시오. 

다음 표는 플랫폼 관리 역할에 맵핑되는 조치에 대해 자세히 설명합니다. 플랫폼 관리 역할을 통해 사용자는 서비스 리소스에 대한 태스크를 플랫폼 레벨에서 수행할 수 있습니다. 예를 들어 서비스에 대한 사용자 액세스 권한을 지정하고, 인스턴스를 작성 또는 삭제하며, 인스턴스를 애플리케이션에 바인드할 수 있습니다. 

| 플랫폼 관리 역할 | 조치 설명 | 조치 예                                                 |
|--------------------------|------------------------|-----------------------------------------------------------------|
| 뷰어                   |설명            | <ul><li>예 1</li><li>예 2</li></ul>                   |
| 편집자                   |설명            |<ul><li>예 1</li><li>예 2</li></ul>                    |
| 운영자                 |설명            | <ul><li>예 1</li><li>예 2</li><li>예 3</li></ul> |
| 관리자            |설명            |<ul><li>예 1</li><li>예 2</li><li>예 3</li></ul>  |
{: caption="표 1. IAM 사용자 역할 및 조치" caption-side="top"}


다음 표는 서비스 액세스 역할에 맵핑되는 조치에 대해 자세히 설명합니다. 서비스 액세스 역할을 통해 사용자는 {{site.data.keyword.aios_short}}에 액세스하고 {{site.data.keyword.aios_short}} API를 호출할 수 있습니다. 

| 서비스 액세스 역할 | 조치 설명 | 조치 예                                                 |
|---------------------|------------------------|-----------------------------------------------------------------|
| 독자              |설명            | <ul><li>예 1</li><li>예 2</li></ul>                   |
| 작성자              |설명            |<ul><li>예 1</li><li>예 2</li></ul>                    |
| 관리자             |설명            | <ul><li>예 1</li><li>예 2</li><li>예 3</li></ul> |
{: caption="표 2. IAM 서비스 액세스 역할 및 조치" caption-side="top"}


UI에서 사용자 역할을 지정하는 방법은 [리소스에 대한 액세스 관리](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)를 참조하십시오. 

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
