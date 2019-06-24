---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: Microsoft Azure, ml, machine learning, services

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Microsoft Azure ML Studio 인스턴스 지정
{: #connect-azure}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Microsoft Azure ML Studio 인스턴스를 지정하는 것입니다. Azure ML Studio 인스턴스는 AI 모델과 배치를 저장하는 곳입니다.
{: shortdesc}

## Azure ML Studio 인스턴스 연결
{: #ca-connect}

{{site.data.keyword.aios_short}}은 Azure ML Studio 인스턴스의 AI 모델 및 배치에 연결합니다.

1.  {{site.data.keyword.aios_short}} 도구의 홈 페이지에서 **시작**을 클릭하십시오.

    ![홈 페이지](images/gs-config-start.png)

1.  **Microsoft Azure ML Studio** 타일을 선택하고 **다음**을 클릭하십시오.

    ![Azure ML Studio 선택](images/connect-azure.png)

1.  인증 정보 입력:

    Microsoft Azure 인증 정보를 가져오는 방법에 대한 지침은 [How to: Use the portal to create an Azure AD application and service principal that can access resources ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window}를 참조하십시오.
    {: note}

    ![Azure ML Studio 신임 정보 입력](images/connect-azure-cred.png)

1.  **다음**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택하십시오.

    ![MS Azure 배치 모델 선택](images/connect-azure-deploys.png)

1.  **다음**을 클릭하십시오.

### 다음 단계
{: #ca-next}

{{site.data.keyword.aios_short}}이 [데이터베이스를 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db)할 준비가 되었습니다.
