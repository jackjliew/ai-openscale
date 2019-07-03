---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Amazon SageMaker ML 서비스 인스턴스 지정
{: #csm-connect}

{{site.data.keyword.aios_short}} 도구에서 첫 번째 단계는 Amazon SageMaker 서비스 인스턴스를 지정하는 것입니다. Amazon SageMaker 서비스 인스턴스는 사용자의 AI 모델 및 배치를 저장하는 곳입니다.
{: shortdesc}

Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)을 참조하십시오. 

## Amazon SageMaker 서비스 인스턴스 연결
{: #csm-config}

{{site.data.keyword.aios_short}}은 Amazon SageMaker 서비스 인스턴스에서 AI 모델 및 배치에 연결됩니다.

1.  {{site.data.keyword.aios_short}} 도구의 홈 페이지에서 **시작**을 클릭하십시오.

    ![홈 페이지](images/gs-config-start.png)

1.  **Amazon SageMaker** 타일을 선택하고 **다음**을 클릭하십시오.

    ![Amazon SageMaker 서비스 선택](images/connect-sage.png)

1.  인증 정보 입력:

    - 액세스 키 ID: 사용자의 AWS 액세스 키 ID `aws_access_key_id`로, 사용자의 신원을 확인하고 AWS에 대한 호출을 인증하고 권한을 부여합니다. 
    - 시크릿 액세스 키: 사용자의 AWS 시크릿 액세스 키 `aws_secret_access_key`로, 사용자의 신원을 확인하고 AWS에 대한 호출을 인증하고 권한을 부여하는 데 필요합니다. 
    - 지역: 액세스 키 ID가 작성된 영역을 입력하십시오. 키는 작성된 영역에서 저장 및 사용되고 다른 영역으로 전송할 수는 없습니다. 

    ![Amazon SageMaker 서비스 인증 정보 입력](images/connect-sage-cred.png)

1.  **다음**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}}이 배치된 모델을 나열합니다. 모니터할 모델을 선택하십시오.

    ![Amazon SageMaker 배치 모델 선택](images/connect-sage-deploys.png)

1.  **다음**을 클릭하십시오.

### 다음 단계
{: #csm-next}

{{site.data.keyword.aios_short}}이 [데이터베이스를 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db)할 준비가 되었습니다.
