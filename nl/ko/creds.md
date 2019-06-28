---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 인증 정보 작성
{: #cred-create}

{{site.data.keyword.aios_short}} REST API에 액세스하려면 플랫폼 API 키 및 데이터 마트(서비스 인스턴스) ID가 필수입니다. 플랫폼 API 키는 개별 사용자에게 {{site.data.keyword.cloud_notm}} 내의 리소스에 액세스할 수 있는 기능을 제공합니다.

엔터프라이즈 계정의 경우, 관리자가 데이터 마트를 작성한 다음 기타 사용자를 계정에 초대하여 해당 사용자에게 특정 {{site.data.keyword.aios_short}} 데이터 마트에 대한 액세스 권한을 제공할 수 있습니다. 그러면 사용자가 자신의 플랫폼 API 키를 작성하여 동일한 {{site.data.keyword.aios_short}} 데이터 마트에 액세스할 수 있습니다. 어떠한 충돌이나 보안 위험도 없습니다.

플랫폼 API 키를 작성하려면 다음 단계를 완료하십시오.

- [{{site.data.keyword.cloud_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}){: new_window}에 로그인하십시오.

- **관리** --> **보안** --> **플랫폼 API 키**를 선택하십시오.

    ![플랫폼 API 키](images/cred-api-key.png)

- 플랫폼 API 키를 작성하고 저장하십시오.

데이터 마트 또는 서비스 인스턴스 ID를 찾으려면 다음 단계를 완료하십시오.

- {{site.data.keyword.aios_short}} **구성 --> 요약** 페이지에서 첫 번째 항목이 데이터 마트(서비스 인스턴스) ID입니다.

    ![데이터 마트 ID](images/data-mart-id.png)
