---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Microsoft Azure ML 서비스 프레임워크
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}}에서는 다음 Microsoft Azure Machine Learning 서비스 프레임워크를 완전히 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| 원시 | 분류 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

## {{site.data.keyword.aios_short}}에 Microsoft Azure ML 서비스 추가
{: #frmwrks-azure-add}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 Microsoft Azure ML 서비스와 함께 작동하도록 구성할 수 있습니다. 

- 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [Microsoft Azure ML Studio 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)을 참조하십시오. 
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [Microsoft Azure 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind)을 참조하십시오. 


메타데이터에는 온보드 사용자 페이로드가 필요합니다.
업로드 훈련 데이터에 대한 모니터링을 구성하려면 모델 온보딩 UI를 작성하십시오.
노트북 openscale에는 페이로드 로깅 실행을 위한 정보가 필요합니다.
UI - 새로 고치기

구현자의 책임 

MJS: Lukasz 및 Clifford Chu와 함께 후속 처리 



## 샘플 노트북
{: #frmwrks-azure-smpl-ntbks}

다음 노트북은 Microsoft Azure ML 서비스로 작업하는 방법을 보여줍니다. 

- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [MS Azure 서비스 모델 스코어링 예](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## 추가 탐색
{: #frmwrks-azure-mediumblogs}

[Watson OpenScale로 Azure 기계 학습 모니터](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
