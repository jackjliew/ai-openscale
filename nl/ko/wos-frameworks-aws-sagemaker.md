---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Amazon SageMaker 프레임워크
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}}에서는 다음 Amazon SageMaker 프레임워크를 전적으로 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| 원시 | 분류 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}


## {{site.data.keyword.aios_short}}에 Amazon SageMaker 추가
{: #frmwrks-aws-sage-add}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 Amazon SageMaker와 함께 작동하도록 구성할 수 있습니다.

- 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [Amazon SageMaker 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)을 참조하십시오.
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Amazon SageMaker 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind)을 참조하십시오.


## 샘플 노트북
{: #frmwrks-aws-sage-smpl-ntbks}

다음 노트북은 Amazon SageMaker로 작업하는 방법을 보여줍니다.

- [신용 위험 예측 모델의 작성 및 배치](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## 추가 탐색
{: #frmwrks-aws-sage-mediumblogs}

[Watson OpenScale로 Sagemaker 기계 학습 모니터](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
