---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

{{site.data.keyword.aios_short}}에서는 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820)를 통해 프로비저닝이 수행되는 경우 단일 인스턴스에서 여러 기계 학습 엔진을 지원합니다.
{: shortdesc}

{{site.data.keyword.aios_short}}를 처음 설정할 때 사용자 인터페이스 또는 자동화된 설정 옵션을 사용하여 첫 번째 기계 학습 엔진을 프로비저닝했을 수 있습니다. 기계 학습 엔진을 추가하려면 Python SDK를 사용해야 합니다. 특히 `client.data_mart.bindings.add` 메소드를 사용하여 기계 학습 엔진을 {{site.data.keyword.aios_short}}에 추가할 수 있습니다.

## 바인딩 메소드
{: #fmrk-workaround-multmleng-binding}

Python API `client.data_mart.bindings.add` 메소드를 사용하여 두 개 이상의 기계 학습 엔진을 {{site.data.keyword.aios_short}}에 바인딩할 수 있습니다. 

- {{site.data.keyword.pm_full}} 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

- Azure ML Studio 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

- AWS Sagemaker 기계 학습 엔진을 바인딩하려면 다음 명령을 실행하십시오.

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

모든 바인딩 목록을 보려면 다음과 같이 `list` 메소드를 실행하십시오.

`    client.data_mart.bindings.list()
    `


| uid |이름 | service_type | 작성됨 |
|:---|:---:|:---:|:---:
| e88sl###-####-####-############ | 내 Azure ML Studio 엔진 | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | WML 인스턴스 | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | 내 AWS SageMaker 엔진 | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="표 1. 서비스 바인딩" caption-side="top"}


특정 기계 학습 엔진에 관한 정보는 다음 주제를 참조하십시오.

- [사용자 정의 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).
- [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)
- [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)


실제 노트북의 작동 예는 [{{site.data.keyword.aios_short}} 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)을 참조하십시오.

