---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 편향성 제거 옵션
{: #it-dbo}

{{site.data.keyword.aios_short}}에서는 수동 및 활성이라는 두 가지 편향성 제거 유형을 지원합니다. 수동 편향성 제거는 편향된 정도를 알 수 있도록 해주고, 활성 편향성 제거는 현재 애플리케이션에 대한 모델을 실시간으로 변경하여 편향을 앞으로 전달하지 못하도록 합니다.

- *수동 편향성 제거* - 수동 편향성 제거는 OpenScale에서 매시간 자동으로 자체 수행하는 작업으로, 사용자 개입 없이 발생하기 때문에 수동으로 간주됩니다. {{site.data.keyword.aios_short}}에서 편향성 검사를 수행할 때, 모델의 동작을 분석하고 모델이 편향된 방식으로 작동하고 있는 데이터를 식별함으로써 데이터의 편향성 제거도 함께 수행합니다.

  그런 다음 {{site.data.keyword.aios_short}}이 기계 학습 모델을 빌드하여 모델이 지정된 대 데이터 점에 대해 편향된 방식으로 작동할 가능성이 높은지 여부를 예측합니다. 그런 다음 {{site.data.keyword.aios_short}}이 모델에 의해 수신된 데이터를 매시간 기준으로 분석하여 {{site.data.keyword.aios_short}}이 모델이 편향된 방식으로 작동한다고 판단하는 데이터 점을 찾습니다. 해당 데이터 점에 대해 공정성 속성이 사소한 것부터 중요한 것까지 섭동되고 섭동된 데이터가 예측을 위해 원래 모델로 전송됩니다. 원래 모델의 이 예측이 편향성 제거된 결과로 사용됩니다.

  {{site.data.keyword.aios_short}}이 지난 시간 내에 모델에 의해 수신된 모든 데이터에 대해 이 편향성 제거를 매시간 수행합니다. 또한 편향성 제거된 출력에 대해 공정성을 계산하여 **편향성 제거된 모델** 탭에서 표시합니다.

- *활성 편향성 제거* - 활성 편향성 제거는 REST API 엔드포인트를 통해 편향성이 제거된 결과를 요청하여 애플리케이션으로 가져오는 한 방법으로, 사용자가 비편향된 방식으로 애플리케이션을 실행할 수 있도록 편향성 제거를 실행하고 모델을 변경하라고 {{site.data.keyword.aios_short}}에 적극적으로 지시합니다. 활성 편향성 제거에서는 애플리케이션에서 편향성 제거 REST API 엔드포인트를 활용할 수 있습니다. 이 REST API 엔드포인트는 내부적으로 모델을 호출하여 해당 작동을 확인합니다.

  {{site.data.keyword.aios_short}}에서 편향된 방식으로 모델이 작동함을 발견하면 이전에 언급한 대로 데이터 섭동을 수행하여 원래 모델로 다시 전송합니다. 섭동된 데이터에 대한 원래 모델의 결과가 편향성 제거된 예측으로 리턴됩니다. {{site.data.keyword.aios_short}}이 원래 모델이 편향된 방식으로 작동하지 않는다고 판단하면 {{site.data.keyword.aios_short}}이 원래 모델의 예측을 편향성 제거된 예측으로 리턴합니다. 따라서 이 REST API 엔드포인트를 사용함으로써 애플리케이션이 모델의 편향된 결과를 기반으로 하여 의사결정을 내리지 않음을 보장할 수 있습니다.

편향성 제거된 REST API 엔드포인트를 찾으려면 **편향성 제거된 스코어링 엔드포인트** 링크를 선택하십시오.

![편향성 제거 API 엔드포인트 세부사항 화면이 코드 스니펫 상자에 표시된 cURL 예제와 함께 표시됨](images/insight-debias-api.png)

## 다음 단계
{: #it-dbo-nextsteps}

- 편향성을 줄이려면 감지된 이후에 문제점을 해결하는 새 모델 버전을 빌드해야 합니다. {{site.data.keyword.aios_short}}은 수동 레이블링 테이블에 편향된 레코드를 저장합니다. 이러한 편향된 레코드는 수동으로 레이블링되어야 하며, 이후에 모델은 편향성 제거된 모델의 새 버전을 빌드하기 위해 이 추가 데이터를 사용하여 재훈련을 받아야 합니다. 


