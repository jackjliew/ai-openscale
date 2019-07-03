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

# {{site.data.keyword.aios_short}}와 서드파티 ML 엔진 통합
{: #fmrk-workaround}

{{site.data.keyword.aios_full}}는 Microsoft Azure ML Studio 및 Amazon SageMaker와 같은 외부 기계 학습 서비스 엔진과 통합됩니다.
{: shortdesc}

다음과 같은 방식으로 {{site.data.keyword.aios_short}}를 서드파티 엔진과 통합할 수 있습니다.

- 엔진 바인딩 레벨: 배치를 나열하고 배치 세부사항을 가져올 수 있습니다. 
  
- 배치 등록 레벨: {{site.data.keyword.aios_short}}에서는 {{site.data.keyword.pm_full}} 형식과 같은 필수 형식으로 구독한 배치의 점수를 매기고 동일한 호환 가능 형식으로 출력을 수신할 수 있어야 합니다. {{site.data.keyword.aios_short}}는 입력과 출력 형식을 둘 다 처리하도록 구성해야 합니다.
   

- 페이로드 로깅: 사용자의 애플리케이션에서 트리거하는 배치된 모델의 각 입력과 출력을 페이로드 저장소에 저장해야 합니다. 페이로드 레코드의 형식은 배치 구독 레벨의 이전 섹션에 언급된 동일한 스펙을 따릅니다.
   
   {{site.data.keyword.aios_short}}에서는 편향성, 설명 및 기타를 계산하는 데 이 레코드를 사용합니다. {{site.data.keyword.aios_short}}에서 {{site.data.keyword.aios_short}} 시스템 외부에 있는 사용자 사이트에서 실행되는 트랜잭션을 자동으로 저장할 수 없습니다. {{site.data.keyword.aios_short}}에서 독점 정보를 보호하는 방법 중 하나입니다. {{site.data.keyword.aios_short}} Rest API 또는 Python SDK를 사용하여 보안 데이터에 관해 작업하십시오.
   
## 이 솔루션을 구현하는 단계
{: #fmrk-workaround-steps}

1. [사용자 정의 기계 학습 엔진에 대해 학습합니다.](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine). 
2. [페이로드 로깅을 설정합니다](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload). 
3. [페이로드 로깅을 자동화합니다](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg). 
4. [사용자 정의 기계 학습 엔진 예](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex) 중 하나를 사용하여 사용자 정의 기계 학습 엔진을 설정합니다. 

