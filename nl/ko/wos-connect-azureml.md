---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure studio, ml, machine learning, services, studio

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

1. **구성** 탭에서 **기계 학습 제공자**를 클릭하십시오. 환경에 따라서는 다음 제공자를 모두 보지 못할 수 있습니다. 

   ![지원되는 기계 학습 엔진에 대한 타일과 함께 기계 학습 서비스 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

1.  **Microsoft Azure ML Studio** 타일을 클릭하십시오.

    ![Azure ML Studio 신임 정보 입력](images/connect-azure-cred.png)

1.  인증 정보를 입력한 후 저장하십시오.

    - 클라이언트 ID: 클라이언트 ID의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다.
    - 클라이언트 시크릿: 시크릿의 실제 문자열 값으로, 사용자의 신원을 확인하고 Azure Studio에 대한 호출을 인증하고 권한을 부여합니다.
    - 테넌트: 테넌트 ID는 사용자의 조직에 해당하며 Azure AD의 전용 인스턴스입니다. 테넌트 ID를 찾으려면 계정 이름 위에 마우스 커서를 올려 디렉토리/테넌트 ID를 표시하거나, Azure 포털에서 Azure Active Directory > 특성 >  디렉토리 ID를 선택하십시오.
    - 구독 ID: Microsoft Azure 구독을 고유하게 식별하는 구독 인증 정보입니다. 구독 ID는 모든 서비스 호출의 URI 파트를 구성합니다.
    - 서비스 제공자 인스턴스 이름: 이 서비스 제공자에 지정된 특정 이름입니다. 
    - 설명: (선택사항) 이 서비스 제공자 인스턴스의 일반어 설명입니다. 프로덕션 및 테스트 환경이 있으면 이는 해당 정보를 포함하기에 알맞은 위치입니다. 


    Microsoft Azure 인증 정보를 가져오는 방법에 대한 지침은 [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}를 참조하십시오.
    {: note}

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택한 후 **구성**을 클릭하십시오.

배치를 선택했습니다.

### 다음 단계
{: #ca-next}

이제 {{site.data.keyword.aios_short}}이 [모니터를 구성](/docs/services/ai-openscale?topic=ai-openscale-mo-config)할 준비가 되었습니다.
