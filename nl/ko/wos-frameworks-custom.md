---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# 사용자 정의 ML 프레임워크
{: #frmwrks-custom}

{{site.data.keyword.aios_full}}에서는 다음 사용자 정의 기계 학습 프레임워크를 전적으로 지원합니다.
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| {{site.data.keyword.pm_full}}과 동일 | 분류 | 정형 |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

## {{site.data.keyword.aios_short}}에 사용자 정의 기계 학습 엔진 추가
{: #frmwrks-custom-add}

다음 방법 중 하나를 사용하여 {{site.data.keyword.aios_short}}이 사용자 정의 기계 학습 제공자와 함께 작동하도록 구성할 수 있습니다.

- 사용자 정의 기계 학습 제공자를 {{site.data.keyword.aios_short}}에 처음 추가하는 경우 구성 인터페이스를 사용할 수 있습니다. 자세한 정보는 [사용자 정의 기계 학습 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-co-connect)을 참조하십시오.
- Python SDK를 사용하여 기계 학습 제공자를 추가할 수도 있습니다. 제공자가 둘 이상인 경우 이 방법을 사용해야 합니다. 이를 프로그래밍 방식으로 수행하는 방법은 [사용자 정의 기계 학습 엔진 바인딩](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind)을 참조하십시오.


## 샘플 노트북
{: #frmwrks-custom-smpl-ntbks}

- [Kubernetes 클러스터를 사용하여 사용자 정의 기계 학습 엔진 작성](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [데이터 마트 작성, 모델 배치 모니터링 및 데이터 분석](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## 추가 탐색
{: #frmwrks-custom-mediumblogs}

[Watson OpenScale로 사용자 정의 기계 학습 엔진 모니터](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
