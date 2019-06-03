---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 트랜잭션 설명
{: #ie-ov}

각 배치에 대해 특정 트랜잭션에 대한 데이터의 설명 가능성을 볼 수 있습니다.
{: shortdesc}

## 트랜잭션 설명
{: #ie-view}

선택된 배치 타일의 네비게이터에서 **트랜잭션 설명** 탭(![트랜잭션 설명 탭](images/insight-transact-tab.png))을 선택하고 트랜잭션 ID를 입력하십시오.

스코어링을 위해 모델에 데이터를 전송할 때마다 `X-Global-Transaction-Id` 필드를 설정하여 HTTP 헤더에 트랜잭션 ID를 설정해야 합니다. 이 트랜잭션 ID는 페이로드 테이블에 저장됩니다. 특정 스코어링에 대한 모델 동작의 설명을 찾으려면 해당 스코어링 요청과 연관된 트랜잭션 ID를 지정하십시오. 이 동작은 Watson Machine Learning(WML) 트랜잭션에만 적용되며 비WML 트랜잭션에는 적용되지 않습니다.
{: note}

### {{site.data.keyword.aios_short}}에서 트랜잭션 ID 찾기
{: #ie-find}

1.  배치에 대한 시간 차트에서 마커를 차트를 가로질러 밀고 [특정 시간에 대한 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)에 대한 **세부사항 보기** 링크를 클릭하십시오.
1.  **트랜잭션 보기** 단추를 클릭하여 [트랜잭션 ID 목록을 보십시오](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  목록에서 트랜잭션 ID 중 하나를 복사하여 **트랜잭션 설명** 페이지의 검색 상자에 이를 붙여넣고 Enter를 누르십시오.

    임의의 트랜잭션 ID에 대한 조치 열에서 **설명** 링크를 클릭하는 방법으로도 트랜잭션 ID 목록을 표시할 수 있습니다. 이 경우, 설명 가능성 탭에서 트랜잭션이 열립니다.
    {: note}

  다른 유형의 모델에 대한 설명 예를 보려면 다음 절을 참조하십시오.

  ![설명 가능성 트랜잭션 ID](images/insight-explain-trans-id.png)

## 카테고리 모델 예
{: #ie-class}

이 설명 가능성 예는 보험 청구를 승인하거나 거부하는 2진 분류 모델에 해당됩니다. 이 케이스에서 `DENIED`라는 최종 결과에 긍정적 또는 부정적으로 기여하는 요인을 볼 수 있습니다.

`< 1 year`라는 값을 가진 *POLICY AGE* 특성이 DENIED 결과를 결정하는 데 최대 영향을 미쳤습니다. 이 결과에 기여한 기타 특성은 *CLAIM FREQUENCY*(`High`) 및 *AGE*(`18`)이며 *CAR VALUE*(`$50,000`)는 미미한 영향만 미쳤습니다.

![설명 가능성 2진 분류](images/insight-explain-binary.png)

차트가 트랜잭션의 결과를 판별함에 있어 최대 유효 요인을 표시하는 데 유용한 반면 분류 모델은 `Minimum changes for Approved outcome` 및 `Minimum changes for this outcome` 섹션에 상세한 고급 설명을 포함할 수 있습니다.

회귀, 이미지 및 비정형 텍스트 모델에 대해서는 고급 설명을 사용할 수 없습니다.
{: note}

`Minimum changes for Approved outcome`은 특성의 값이 이 절에 나열된 값으로 변경되면 모델의 예측이 변경됨을 알려줍니다.

이와 마찬가지로 `Minimum changes for this outcome`은 특성의 값이 이 절에 나열된 값으로 변경되더라도 모델의 예측이 변경되지 않음을 알려줍니다.

따라서 이러한 두 값은 설명이 생성되는 데이터 점의 부근에서 모델의 동작에 대해 알려줍니다.

![설명 가능성 2진 분류](images/insight-explain-binary2.png)

## 이미지 모델 예
{: #ie-image}

설명 가능성의 이미지 분류 모델 예의 경우, 예측된 결과에 대해 이미지 중 어느 파트가 긍정적 또는 부정적으로 기여하는지 알려줍니다. 아래 예에서, 오른쪽 이미지는 예측에 긍정적으로 영향을 미치는 파트를 표시하고 왼쪽 이미지는 결과에 긍정적으로 영향을 미치는 파트를 표시합니다.

- {{site.data.keyword.pm_full}}의 경우 기계 학습 게이트웨이를 통해 전송된 섭동된 이미지의 페이로드는 1MB를 초과할 수 없습니다. 제한시간 문제를 방지하려면, 이미지가 125 x 125픽셀을 초과하지 않아야 하며 첫 번째 이미지가 완료되면 두 번째 이미지에 대한 설명이 요청되도록 순차적으로 전송해야 합니다.
{: note}

![설명 가능성 이미지 분류](images/insight-explain-image.png)

## 비정형 텍스트 모델 예
{: #ie-unstruct}

최종적으로, 설명 가능성의 예는 비정형 텍스트를 평가하는 분류 모델을 표시합니다. 설명은 모델 예측에 대한 부정적인 영향 및 긍정적인 영향을 가진 키워드를 표시합니다. 또한 모델에 입력으로 제공된 원래 텍스트에서 식별된 키워드의 위치를 표시합니다.

![설명 가능성 이미지 분류](images/insight-explain-text.png)
