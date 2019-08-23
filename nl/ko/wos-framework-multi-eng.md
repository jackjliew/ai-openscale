---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# 여러 기계 학습 엔진 지원
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}}은 단일 인스턴스 내에 복수의 기계 학습 엔진을 지원합니다. {{site.data.keyword.aios_short}} 대시보드 구성 또는 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820)를 통해 이를 프로비저닝할 수 있습니다.
{: shortdesc}

{{site.data.keyword.aios_short}}를 처음 설정할 때 사용자 인터페이스 또는 자동화된 설정 옵션을 사용하여 첫 번째 기계 학습 엔진을 프로비저닝했을 수 있습니다. 기계 학습 엔진을 추가하려면 Python SDK 또는 {{site.data.keyword.aios_short}} 대시보드의 구성 탭을 사용해야 합니다.

## 대시보드를 사용하여 제공자 추가
{: #fmrk-workaround-multmleng-dashboard}

1. {{site.data.keyword.aios_short}}을 연 후 **구성** 탭에서 **기계 학습 제공자 추가** 단추를 클릭하십시오.

   ![기계 학습 제공자 창에 제공자 추가 단추가 표시됨](images/wos-configure-multi-providers.png)

2. 추가할 제공자의 타일을 클릭한 후 **다음**을 클릭하십시오.

   ![기계 학습 제공자 선택 화면이 표시됨](images/wos-machine-learning-providers-selection.png)

3. 필수 정보(예: 인증 정보)를 입력한 후 **저장**을 클릭하십시오.

구성을 저장하고 나면 대시보드로 이동하거나 배치를 선택하거나 모니터를 구성하는 옵션이 제공됩니다.

## 기계 학습 제공자 편집
{: #fmrk-workaround-editingproviders-dashboard}

기계 학습 제공자를 편집해야 합니까? 타일 메뉴 ![타일 메뉴 아이콘](images/v-three-dots.png) 아이콘을 클릭한 후 **세부사항 보기 및 편집**을 클릭하십시오. 

   ![기계 학습 제공자 보기 및 편집 옵션이 표시됨](images/wos-machine-learning-providers-edit.png)

## Python SDK 바인딩 메소드를 사용하여 기계 학습 제공자 추가
{: #fmrk-workaround-multmleng-binding}

Python API `client.data_mart.bindings.add` 메소드를 사용하여 두 개 이상의 기계 학습 엔진을 {{site.data.keyword.aios_short}}에 바인딩할 수 있습니다. 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- {{site.data.keyword.pm_full}} 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Azure ML Studio 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- AWS Sagemaker 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML 서비스
{: #fmrk-workaround-multmleng-binding-azureservice}

- Azure ML 서비스 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

  `binding_uid_4 = client.data_mart.bindings.add('My Azure ML Service engine', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### 기계 학습 제공자 목록 생성
{: #fmrk-workaround-multmleng-binding-list}

모든 바인딩 목록을 보려면 다음과 같이 `list` 메소드를 실행하십시오.

`    client.data_mart.bindings.list()
    `


| uid |이름 | service_type | 작성됨 |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | 내 Azure ML 서비스 엔진 | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | 내 Azure ML Studio 엔진 | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML 인스턴스 | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | 내 AWS SageMaker 엔진 | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="표 1. 서비스 바인딩" caption-side="top"}


특정 기계 학습 엔진에 관한 정보는 다음 주제를 참조하십시오.

- [사용자 정의 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind).
- [Microsoft Azure Machine Learning Studio Engine 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Microsoft Azure 기계 학습 서비스 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


실제 노트북의 작동 예는 [{{site.data.keyword.aios_short}} 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)을 참조하십시오.

