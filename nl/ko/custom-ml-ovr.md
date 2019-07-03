---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 사용자 정의 기계 학습 엔진
{: #fmrk-workaround-customengine}

사용자 정의 기계 학습 엔진에서는 기계 학습 모델과 웹 애플리케이션의 인프라 및 호스팅 기능을 제공합니다. {{site.data.keyword.aios_short}}에서 지원하는 사용자 정의 기계 학습 엔진에서는 다음 요구사항을 준수합니다.

- 두 가지 유형의 REST API 엔드포인트를 노출합니다.

   * 검색 엔드포인트(배치 및 상세 정보의 목록 가져오기)
   * 스코어링 엔드포인트(온라인 및 실시간 스코어링)

- 모든 엔드포인트는 지원될 Swagger 스펙과 호환 가능해야 합니다.

- 배치의 입력 페이로드와 출력은 스펙에 설명된 JSON 파일 형식을 준수해야 합니다.

이 단계에서는 `BasicAuth` 또는 `none` 형식만 지원됩니다.
{: Note}

다음 예제에서는 REST API 엔드포인트 스펙을 보여줍니다.

![REST API 엔드포인트 스펙은 Swagger 문서에서 표시됨](images/wosdeployments.png)


다음 예제에서는 입력 페이로드의 형식을 보여줍니다.

![입력 페이로드 예제 표시](images/wosinputdata.png)


## 언제 사용자 정의 기계 학습 엔진을 선택하는 것이 가장 좋습니까?
{: #fmrk-workaround-enging-choice}

사용자 정의 기계 학습 엔진은 다음 상황이 참일 때 선택하는 것이 가장 좋습니다.

- 기계 학습 모델을 제공하기 위해 사전 설정된 사용 가능한 제품을 사용하고 있지 않습니다. 해당 작업을 수행하도록 고유 시스템을 개발했습니다. 따라서 {{site.data.keyword.aios_short}}에서 이 시스템을 직접 지원하지 않습니다. 
- 서드파티에서 사용 중인 서비스 엔진은 {{site.data.keyword.aios_short}}에서 아직 지원하지 않습니다. 이 경우 사용자 정의 기계 학습 엔진을 원래 또는 고유 배치에 사용할 랩퍼로 개발하는 것을 고려하십시오.

## 다음 단계
{: #fmrk-workaround-nxt-steps-over}

[사용자 정의 기계 학습 엔진 예](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex) 중 하나를 사용하여 사용자 고유의 솔루션을 구현하십시오. 
