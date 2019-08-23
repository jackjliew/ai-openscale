---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API, datamart ID, IDs, binding ID,  deployment ID, subscription ID

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

# {{site.data.keyword.aios_short}}의 인증 정보 작성
{: #cred-create}

{{site.data.keyword.aios_full}} REST API에 액세스하려면 플랫폼 API 키와 서비스 인스턴스라고도 하는 데이터 마트 ID가 필요합니다. 플랫폼 API 키는 개별 사용자에게 {{site.data.keyword.cloud_notm}} 내의 리소스에 액세스할 수 있는 기능을 제공합니다.
{: shortdesc}

엔터프라이즈 계정의 경우, 관리자가 데이터 마트를 작성하고 사용자를 계정에 초대하며 해당 사용자에게 특정 {{site.data.keyword.aios_short}} 데이터 마트에 대한 액세스 권한을 제공할 수 있습니다. 그런 다음 사용자가 고유 플랫폼 API 키를 작성하고 동일한 {{site.data.keyword.aios_short}} 데이터 마트에 액세스할 수 있습니다. 충돌 또는 보안 위험이 없습니다.

## 플랫폼 API 키 작성
{: #cred-create-apikey}

IBM Cloud API 키를 작성하려면 다음 단계를 완료하십시오. 

- [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}에 로그인하십시오.
- **관리** --> **액세스(IAM)** --> **{{site.data.keyword.cloud_notm}} API 키**를 선택하십시오. 
- **IBM Cloud API 키 작성** 단추를 클릭하십시오. 
- 키에 이름과 설명을 부여하고 **작성**을 클릭하십시오. 

## 서비스 ID 찾기:
{: #cred-find-datamart-id}

배치할 **모니터 구성**을 선택할 때 표시되는 {{site.data.keyword.aios_short}} **페이로드 로깅** 페이지에서 데이터 마트, 배치, 구독 또는 바인딩 ID를 찾으십시오. 

1. 모델 배치 타일을 클릭하십시오. 
2. **모니터 구성** ![구성 아이콘](images/configure-deployment-button.png)을 클릭하십시오. 
3. **페이로드 로깅**을 클릭하십시오. 
4. {{site.data.keyword.aios_short}} **페이로드 로깅** 페이지의 **세부사항** 분할창에서 찾으려는 ID를 찾으십시오. 예: **데이터 마트 ID** 필드: 

    ![데이터 마트 ID](images/data-mart-id.png)

## 명령 콘솔을 사용하여 서비스 인스턴스 인증 정보 작성
{: #cred-creds}

{{site.data.keyword.aios_short}}의 인증 정보를 작성하려면 {{site.data.keyword.cloud_notm}} [명령 콘솔](/docs/cli?){: external}을 사용하여 다음 단계를 완료하십시오.

1. 다음 명령을 실행하여 API 키를 검색하십시오.

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    다음 정보가 표시됩니다.

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```

2. {{site.data.keyword.cloud_notm}} 계정에서 사용 중인 리소스 그룹을 확인하십시오.

   1. 대시보드로 이동하십시오. 
   2. **탐색 메뉴**에서 **리소스 목록**을 클릭하십시오. 
   3. **그룹** 열에서 **그룹 또는 조직별 필터링** 드롭 다운 선택사항을 클릭하고 **기본값** 선택란을 설정하십시오. 

  ![클라우드의 리소스 그룹](images/cloud-resource.png)

  `기본` 리소스 그룹을 사용 중이지 않으면 다음 명령을 실행하여 {{site.data.keyword.aios_short}}의 인증 정보를 가져오십시오.

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  여기서 `myResourceGroup`은 {{site.data.keyword.aios_short}} 인스턴스와 연관된 리소스 그룹의 이름입니다.

3. 다음 명령을 실행하여 {{site.data.keyword.aios_short}} 인스턴스 ID를 검색하십시오.

    ```curl
    ibmcloud resource service-instance '<Your_Watson_OpenScale_instance_name>'
    ```

    **참고**: Windows에서 {{site.data.keyword.cloud_notm}} 명령 콘솔을 사용하는 경우 이전 명령에서 작은따옴표(')를 큰따옴표(")로 바꾸십시오.

    다음 정보가 표시됩니다.

    ```bash
    Name:                  AI OpenScale-my_instance
    ID:                    crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Location:              us-south
    Service Name:          aiopenscale
    Service Plan Name:     lite
    Resource Group Name:   Default
    State:                 active
    Type:                  service_instance
    Sub Type:
    Tags:
    Created at:            2018-09-17T13:58:43Z
    Updated at:
    ```

    `GUID` 값은 {{site.data.keyword.aios_short}} 인스턴스 ID입니다.
        
## 다음 단계
{: #cred-create-next-steps}

기계 학습 제공자를 지정하십시오.

- [IBM Watson Machine Learning 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [Microsoft Azure ML Studio 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [Microsoft Azure ML 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)
- [Amazon SageMaker ML 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [사용자 정의 ML 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-co-connect)
