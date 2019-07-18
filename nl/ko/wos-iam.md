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

## Identity and Access Management 역할 및 조치

계정의 사용자에 대한 {{site.data.keyword.aios_full}} 서비스 인스턴스에 대한 액세스는 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)을 통해 제어됩니다. 계정의 {{site.data.keyword.aios_short}} 서비스에 액세스하는 모든 사용자에게는 IAM 역할이 정의된 액세스 정책을 지정해야 합니다. 정책에 따라 사용자가 선택한 서비스 또는 인스턴스의 컨텍스트 내에서 수행할 수 있는 조치가 결정됩니다. 허용되는 조치는 {{site.data.keyword.Bluemix_notm}} 서비스를 통해 서비스에 대해 수행 가능한 오퍼레이션으로 사용자 정의되고 정의됩니다. 그런 다음 조치가 IAM 사용자 역할에 맵핑됩니다.

정책을 사용하면 서로 다른 레벨에서 액세스 권한을 부여할 수 있습니다. 몇 가지 옵션은 다음과 같습니다. 

* 계정에서 제공하는 서비스의 모든 인스턴스에 대한 액세스
* 계정에서 제공하는 개별 서비스 인스턴스에 대한 액세스
* 인스턴스 내 특정 리소스에 대한 액세스

액세스 정책의 범위를 정의한 후에는 사용자의 액세스 레벨을 결정하는 역할을 지정하십시오. {{site.data.keyword.aios_short}} 서비스 내에서 각 역할이 허용하는 조치를 설명하는 다음 표를 검토하십시오.

플랫폼 관리 역할을 사용하면 계정 내 및 서비스에서 플랫폼 조치를 수행하기 위해 필요한 다양한 레벨의 권한을 사용자에게 지정할 수 있습니다. 예를 들어, 카탈로그 리소스에 대해 지정되는 플랫폼 관리 역할은 사용자가 서비스 인스턴스 작성, 삭제, 편집 및 보기 등의 조치를 완료할 수 있게 합니다. 또한 계정 관리 서비스에 대해 지정되는 플랫폼 관리 역할은 사용자가 사용자 초대 및 제거, 리소스 그룹에 대한 작업 및 비용 청구 정보 보기 등의 조치를 완료할 수 있게 합니다. 계정 관리 서비스에 대한 자세한 정보는 [계정 관리 서비스에 대한 액세스 지정](/docs/iam?topic=iam-account-services#account-services)을 참조하십시오. 

정책 작성 시 적용되는 모든 역할을 선택하십시오. 각각의 역할은 별도의 조치를 완료할 수 있게 하며 더 작은 역할의 조치는 상속하지 않습니다.
{: tip}

다음 표에서는 카탈로그 리소스 및 리소스 그룹의 컨텍스트 내에서 사용자가 취할 수 있는 플랫폼 관리 조치 중 일부에 대한 예를 제공합니다. 각 카탈로그 오퍼링에 대한 문서를 참조하여 사용 중인 서비스의 컨텍스트 내에서 사용자에게 역할을 적용하는 방법을 이해하십시오. 


|  | IAM 사용 서비스 중 하나 또는 모두 | 리소스 그룹의 선택된 서비스 | 선택된 리소스 그룹 |
|:--------------|:------------|:-------------|:-------------|
| 뷰어 역할 | 인스턴스, 별명, 바인딩 및 인증 정보 보기 | 리소스 그룹의 지정된 인스턴스만 보기 | 리소스 그룹 보기 |
| 운영자 역할 | 인스턴스 보기 및 별명, 바인딩 및 인증 정보 관리 | 해당사항 없음 | 해당사항 없음 |
| 편집자 역할 | 인스턴스 작성, 삭제, 편집 및 보기. 별명, 바인딩 및 인증 정보 관리 | 리소스 그룹의 지정된 인스턴스만 작성, 삭제, 편집, 일시중단, 재개, 보기 및 바인딩 | 리소스 그룹의 이름 보기 및 편집 |
| 관리자 역할 | 서비스에 대한 모든 관리 조치 | 리소스 그룹의 지정된 인스턴스에 대한 모든 관리 조치 | 리소스 그룹에 대한 액세스 보기, 편집 및 관리 |
| 클러스터 관리자 역할({{site.data.keyword.wos4d_full}}에만 해당됨) | IBM Cloud Private 플랫폼에 대한 완전한 액세스를 가짐 | 리소스 그룹의 지정된 인스턴스에 대한 완전한 액세스를 가짐 | 클러스터 관리자만 완료할 수 있는 조치: LDAP 디렉토리에 연결, 사용자 추가 및 사용자에게 IAM 역할 지정, 모든 네임스페이스에서 워크로드, 인프라 및 애플리케이션 관리, 네임스페이스 작성, 할당량 지정, 팟(Pod) 보안 정책 추가, 내부 Helm 저장소 추가, 내부 Helm 저장소 삭제, 내부 Helm 저장소에 Helm 차트 추가, 내부 Helm 저장소에서 Helm 차트 제거, 내부 및 외부 Helm 저장소 동기화 |
{: row-headers}
{: class="comparison-table"}
{: caption="표 1. 계정의 서비스에 대한 예제 플랫폼 관리 역할 및 조치" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


{{site.data.keyword.aios_short}}에 대한 사용자 액세스 및 REST API 호출 기능을 허용하는 서비스 액세스 역할의 경우 {{site.data.keyword.aios_short}}은 선행 표에 나열된 플랫폼 관리 역할을 따릅니다. UI에서 사용자 역할을 지정하는 방법은 [리소스에 대한 액세스 관리](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)를 참조하십시오.

 
