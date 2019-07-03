---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Microsoft Azure, ml, machine learning, services

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

# Microsoft Azure ML Studio 인스턴스 지정
{: #connect-azure}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Microsoft Azure ML Studio 인스턴스를 지정하는 것입니다. Azure ML Studio 인스턴스는 AI 모델과 배치를 저장하는 곳입니다.
{: shortdesc}

Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)을 참조하십시오. 

## Azure ML Studio 인스턴스 연결
{: #ca-connect}

{{site.data.keyword.aios_short}}은 Azure ML Studio 인스턴스의 AI 모델 및 배치에 연결합니다.

1.  {{site.data.keyword.aios_short}} 도구의 홈 페이지에서 **시작**을 클릭하십시오.

    ![홈 페이지](images/gs-config-start.png)

1.  **Microsoft Azure ML Studio** 타일을 선택하고 **다음**을 클릭하십시오.

    ![Azure ML Studio 선택](images/connect-azure.png)

1.  인증 정보 입력:

    - 클라이언트 ID: 클라이언트 ID의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다. 
    - 클라이언트 시크릿: 시크릿의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다. 
    - 테넌트: 테넌트 ID는 사용자의 조직에 해당하며 Azure AD의 전용 인스턴스입니다. 테넌트 ID를 찾으려면 계정 이름 위에 마우스 커서를 올려 디렉토리/테넌트 ID를 표시하거나, Azure 포털에서 Azure Active Directory > 특성 >  디렉토리 ID를 선택하십시오. 
    - 구독 ID: Microsoft Azure 구독을 고유하게 식별하는 구독 인증 정보입니다. 구독 ID는 모든 서비스 호출의 URI 파트를 구성합니다. 

    Microsoft Azure 인증 정보를 가져오는 방법에 대한 지침은 [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}를 참조하십시오.
    {: note}

    ![Azure ML Studio 신임 정보 입력](images/connect-azure-cred.png)

1.  **다음**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택하십시오.

    ![MS Azure 배치 모델 선택](images/connect-azure-deploys.png)

1.  **다음**을 클릭하십시오.

### 다음 단계
{: #ca-next}

{{site.data.keyword.aios_short}}이 [데이터베이스를 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db)할 준비가 되었습니다.
