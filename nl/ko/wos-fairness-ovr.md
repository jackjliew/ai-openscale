---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 공정성 메트릭 개요
{: #anlz_metrics_fairness}

{{site.data.keyword.aios_full}} 공정성 모니터링을 사용하여 모델에서 생성한 결과가 모니터 대상 그룹에 공정한지 여부를 판별할 수 있습니다. 공정성 모니터링이 사용으로 설정된 경우 기본적으로 1시간마다 메트릭 세트를 생성합니다. 필요한 경우 **품질 지금 확인** 단추를 클릭하거나 Python 클라이언트를 사용하여 이러한 메트릭을 생성할 수 있습니다.
{: shortdesc}

{{site.data.keyword.aios_short}}에서는 알려진 보호된 속성이 모델에 존재하는지 여부를 자동으로 식별합니다. {{site.data.keyword.aios_short}}에서 이러한 속성을 발견할 경우, 프로덕션 시 잠재적으로 중요한 속성에 대한 편향을 추적할 수 있도록 존재하는 각 속성에 대해 편향 모니터를 구성할 것을 자동으로 권장합니다. 

현재 {{site.data.keyword.aios_short}}은 다음 보호된 속성에 대한 모니터를 발견하고 권장합니다. 

- 성별
- 인종
- 결혼 여부
- 연령
- 우편번호

보호된 속성을 발견하는 것 이외에도, {{site.data.keyword.aios_short}}에서는 각 속성 내에서 모니터되는 값과 참조 값으로 설정할 값도 권장합니다. 따라서 예를 들어 {{site.data.keyword.aios_short}}에서는 "성별" 속성 내에서 "Woman" 및 "Non-Binary"는 모니터되는 값이 되고 "Male"은 참조 값이 되도록 편향 모니터를 구성할 것을 권장합니다. 권장사항을 변경하려는 경우 편향 구성 패널을 통해 이를 편집할 수 있습니다. 

권장되는 편향 모니터는 구성 속도를 높이고 사용자의 AI 모델에서 중요한 속성에 대한 공정성을 확인하는 데 도움이 됩니다. 운영자들이 알고리즘 편향성에 더 높은 관심을 두기 시작하면서 조직의 모델이 어느 정도의 성과를 내는지와 모델이 특정 그룹에 대해 불공평한 결과를 생성하는지 여부를 조직에서 명확하게 이해하는 것이 더욱 중요해졌습니다.

## 공정성 이해
{: #mf-understand}

{{site.data.keyword.aios_short}}은 런타임 시에 배치 모델의 편향성을 검사합니다. 배치된 모델에 대한 편향성을 발견하려면 아래의 [공정성 모니터 구성](#mf-config) 섹션에서 자세히 설명하는 것과 같이 연령 또는 성별 등의 공정성 속성을 정의해야 합니다.

{{site.data.keyword.aios_short}}에서 편향성 검사를 사용할 수 있도록 {{site.data.keyword.pm_short}}에서 모델 또는 함수에 대한 출력 스키마를 반드시 지정해야 합니다. 출력 스키마는 `store_model` API의 메타데이터 파트에서 `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` 특성을 사용하여 지정할 수 있습니다. 자세한 정보는 [{{site.data.keyword.pm_full}}클라이언트 문서](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}를 참조하십시오.

### 작동 방식
{: #mf-works}

공정성 모니터를 구성하기 전에 이해해야 하는 몇 가지 중요한 개념이 있습니다.

- 공정성 속성은 모델이 편향성을 보일 수 있음을 나타내는 모델 속성입니다. 예를 들어, 공정성 속성 **`Gender`**의 경우, 모델이 특정 성별 값(`Female`, `Transgender` 등)에 대해 편향될 수 있습니다. 공정성 속성의 또 다른 예로는 **`Age`**가 있으며 모델이 `18 - 25` 등의 연령 그룹에서 편향성을 나타낼 수 있습니다.

- 참조/모니터됨 값: 공정성 속성의 값은 참조 및 모니터됨이라는 두 개의 개벌 카테고리로 나뉩니다. 모니터되는 값은 구별할 수 있는 가능성이 높은 값입니다. **`Gender`**와 같은 공정성 속성의 경우, 모니터되는 값이 `Female` 및 `Transgender`일 수 있습니다. **`Age`**와 같은 숫자 공정성 속성의 경우, 모니터되는 값이 `[18-25]`일 수 있습니다. 지정된 공정성 속성에 대한 모든 기타 값은 참조 값으로 간주됩니다. 예를 들어, `Gender=Male` 또는 `Age=[26,100]`입니다.

- 선호/비선호 결과: 모델의 결과가 선호 또는 비선호로 분류됩니다. 예를 들어, 모델이 한 개인이 대출을 받을 수 있는지 여부를 예측하는 경우, 선호 결과는 `Loan Granted` 또는 `Loan Partially Granted`인 반면 비선호 결과는 `Loan Denied`일 수 있습니다. 따라서 선호 결과가 긍정적인 결과로 간주되는 반면 비선호 결과는 부정적인 것으로 간주됩니다.

{{site.data.keyword.aios_short}} 알고리즘은 페이로드 로깅 테이블에 있는 최근 `N`개의 레코드를 사용하여 매시간 기준으로 편향성을 계산합니다. `N`의 값은 공정성을 구성할 때 지정됩니다. 알고리즘은 최근 `N`개의 레코드를 섭동하여 추가 데이터를 생성합니다.

섭동은 공정성 속성의 값을 참조에서 모니터로 또는 반대로 변경하여 수행됩니다. 섭동된 데이터는 작동을 평가하기 위해 모니터로 전송됩니다. 알고리즘은 페이로드 테이블 내의 최근 `N`개의 레코드와 섭동된 데이터에 대한 모델의 동작을 관찰하여 모델이 편향된 방식으로 작동하는지 여부를 결정합니다.

결합된 이 데이터 세트 전체에 걸쳐 모니터되는 클래스의 선호 결과의 백분율이 지정된 임계값 차이 이상으로 참조 클래스에 대한 선호 결과의 백분율 미만이면 모델이 편향된 것으로 간주됩니다. 이 임계값은 공정성을 구성할 때 지정됩니다.

공정성 값은 100% 보다 클 수 있습니다. 이는 모니터 대상 그룹이 참조 그룹보다 많은 선호 결과를 수신했음을 의미합니다. 또한, 새 스코어링 요청이 전송되지 않는 경우에는 공정성 값이 변경되지 않습니다.
{: note}

### 계산법
{: #mf-bias-math}

{{site.data.keyword.aios_short}}에서 사용되는 공정성 메트릭은 차별적 효과입니다.즉, 비권한 그룹이 특정 결과를 수신하는 비율을 나타내거나 권한 그룹이 동일한 결과를 수신하는 비율과 결과를 비교할 때 사용되는 측정 단위입니다.

차별적 효과를 계산하는 데 사용되는 수학 공식은 다음과 같습니다.

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
차별적 효과 =   ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

여기서 `num_positives`는 양의 결과를 수신한 그룹 내 개인의 수입니다. 예를 들어 privileged=False는 unprivileged이고, privileged=True는 privileged입니다. num_instances는 그룹 내 개인의 총계입니다.

그 결과는 백분율입니다. 즉, 비권한 그룹이 양의 결과를 수신한 비율 대 권한 그룹이 양의 결과를 수신한 비율을 나타내는 백분율입니다. 예를 들어 신용 위험 모델이 비권한 신청자의 80% 및 권한 신청자의 100%에 "위험 없음" 예측을 지정할 경우, 해당 모델의 차별적 효과는 80%({{site.data.keyword.aios_short}}의 공정성 스코어로 표시됨)입니다.

{{site.data.keyword.aios_short}}에서 양의 결과는 선호 결과로 지정되고, 음의 결과는 비선호 결과로 지정됩니다. 권한 그룹은 참조 그룹으로 지정되고, 비권한 그룹은 모니터 대상 그룹으로 지정됩니다.


### 편향성 시각화 ![베타 태그](images/beta.png)
{: #mf-monitor-bias-viz}

잠재적 편향성이 발견된 경우 {{site.data.keyword.aios_short}}은 여러 기능을 수행하여 편향성이 실제인지 여부를 확인합니다. {{site.data.keyword.aios_short}}은 모니터된 값을 참조 값으로 플립한 후 모델을 통해 이 새 레코드를 실행하여 모니터를 섭동합니다. 그리고 이는 결과 출력을 편향성 제거된 출력으로 표면화합니다. 또한 {{site.data.keyword.aios_short}}은 새도우 편향성 제거된 모델을 훈련시키며, 이는 다시 모델이 편향된 예측을 작성할 때 발견에 사용됩니다. 

공정성과 정확성을 계산하기 위해 서로 다른 두 개의 데이터 세트가 사용됩니다. 공정성은 페이로드 + 섭동된 데이터를 사용하여 계산됩니다. 정확성은 피드백 데이터를 사용하여 계산됩니다. 정확성을 계산하기 위해서는 {{site.data.keyword.aios_short}}에 수동으로 레이블이 지정된 데이터(피드백 테이블에만 표시됨)가 필요합니다.

이러한 결정의 결과는 다음 보기가 포함된 편향성 시각화에서 사용 가능합니다. (지원할 데이터가 있는 경우에만 보기가 나타남)

- **페이로드 + 섭동됨**: 선택한 시간 동안 수신된 스코어링 요청 및 평가에 필요한 최소 레코드 수가 충족되지 않은 경우 이전 시간의 추가 레코드를 포함합니다. 모니터 대상 기능의 값이 변경되는 경우 모델의 응답을 테스트하는 데 사용되는 추가적인 섭동된/합성된 레코드가 포함됩니다.

   다음 페이로드 및 섭동된 세부사항을 기록해 두십시오.

   - 페이로드 테이블에서 이 시간에 읽힌 레코드의 수
   - 이전 시간에서 읽는 추가 레코드(예를 들어, 공정성 구성의 `min_records` 값이 1000으로 설정되어 있고 최소 요구사항을 충족시키기 위해 오후 2시에서 3시 사이에 10개 레코드만 추가되는 경우, 시스템은 추가로 이전 시간의 990개 레코드를 읽습니다.)
   - 공정성 속성별 섭동된 레코드 수
   - 편향성을 계산해야 하는 데이터 프레임의 가장 오래된 레코드 시간소인
   - 편향성을 계산해야 하는 데이터 프레임의 가장 최신 레코드 시간소인

  ![페이로드 및 섭동됨 예](images/payload&perturbed.png)



- **페이로드**: 선택한 시간 동안 모델에서 수신한 실제 스코어링 요청입니다.

   다음 페이로드 세부사항을 기록해 두십시오.
   
   - 페이로드 테이블에서 편향성 제거된 오퍼레이션이 수행되는/읽는 레코드의 수
   - 편향성을 계산해야 하는 데이터 프레임의 가장 오래된 레코드 시간소인
   - 편향성을 계산해야 하는 데이터 프레임의 가장 최신 레코드 시간소인


  ![페이로드 데이터의 예](images/payload.png)

- **훈련**: 모델을 훈련시키는 데 사용되는 훈련 데이터 레코드입니다.

   다음 훈련 세부사항을 기록해 두십시오.
   
   - 훈련 데이터 레코드의 수. 훈련 데이터는 한번 읽혀지며 분포는 `subscription/fairness_configuration` 변수에 저장됩니다. 분포를 계산하는 동안 훈련 데이터 레코드의 수를 찾아서 동일한 분포에 저장해야 합니다. 또한 훈련 데이터가 변경되는 경우(`POST /data_distribution` 명령이 다시 실행되는 경우를 의미함) 이 값은 `fairness_configuration/training_data_distribution` 변수에서 업데이트됩니다. 메트릭을 전송하는 동안 이 값도 전송해야 합니다.
   - 훈련 데이터가 마지막으로 처리되는 시간(첫 번째 및 후속 업데이트)

  ![훈련 데이터의 예](images/training.png)
   

   
- **편향성 제거됨**: 런타임 및 섭동된 데이터를 처리한 후 편향성 제거 알고리즘의 결과입니다. **편향성 제거됨** 단일 선택 단추를 선택하면 편향성 제거된 모델 대 프로덕션 내 모델의 변경사항을 표시합니다. 차트는 그룹에 대해 개선된 결과 상태를 반영합니다. 


   다음 편향성 제거됨의 세부사항을 기록해 두십시오.
   
   - 페이로드 테이블에서 편향성 제거된 오퍼레이션이 수행되는/읽는 레코드의 수
   - 편향을 수행하기 위해 읽혀지는 추가 레코드 및 그로 인해 편향성 제거된 레코드 수. `Payload + Perturbed` 선택의 수와 동일한 수입니다.
   - 공정성 속성별 섭동된 레코드 수
   - 편향성을 계산해야 하는 데이터 프레임의 가장 오래된 레코드 시간소인
   - 편향성을 계산해야 하는 데이터 프레임의 가장 최신 레코드 시간소인
   - 이전 및 이후 공정성 값은 편향성 제거됨 보기의 헤더 부분에 표시됩니다. 
      - **이후** 정확성은 피드백 데이터를 가져온 후 활성 편향성 제거 API로 전송하여 계산됩니다. 이 API는 편향성 제거된 예측을 리턴합니다. 피드백 데이터에는 수동 레이블도 포함되어 있습니다. 수동 레이블은 정확성을 계산하기 위해 편향성 제거된 예측과 비교됩니다. 이 API는 편향성 제거된 예측을 리턴합니다. 피드백 테이블에도 수동 레이블이 포함되어 있습니다. 수동 레이블은 정확성을 계산하기 위해 편향성 제거된 예측과 비교됩니다. 
      - **이전** 정확성은 동일한 피드백 데이터를 사용하여 계산됩니다. 이전 정확성 계산을 위해 피드백 데이터를 모델로 전송하여 예측을 가져온 후 예측 값을 수동 레이블과 비교하여 정확성을 가져옵니다.

  ![편향성 제거된 데이터의 예](images/debiased.png)
  
### 예
{: #mf-ex1}

`Gender=Male`(참조 값)인 데이터 점을 고려하면 모델이 선호 결과를 예측하나 `Gender`를 `Female`(모니터되는 값)로 변경하여 섭동된 레코드인 경우, 모든 기타 특성은 동일하게 유지되나 모델이 비선호 결과를 예측합니다. (페이로드 테이블 내의 최근 `N`개의 레코드 더하기 섭동된 데이터에 걸쳐) 모델에 편향된 방식으로 작동하는 데이터 점이 충분한 경우, 모델이 전체적으로 편향성을 보인다고 합니다.

### 지원되는 모델
{: #mf-supmo}

 {{site.data.keyword.aios_short}}은 특성 벡터 내에 일부 종류의 정형 데이터를 예상하는 모델 및 Python 함수에 대해서만 편향성 발견을 지원합니다.

공정성 메트릭은 다음 정보를 기반으로 계산됩니다.

- 스코어링 페이로드 데이터

적합한 모니터링을 위해 모든 스코어링 요청을 {{site.data.keyword.aios_short}}에도 기록해야 합니다. 페이로드 데이터 로깅은 {{site.data.keyword.pm_full}} 엔진에 대해 자동으로 설정되어 있습니다.

다른 기계 학습 엔진의 경우 페이로드 데이터를 Python 클라이언트 또는 REST API를 사용하여 제공할 수 있습니다.

{{site.data.keyword.pm_full}} 이외의 기계 학습 엔진의 경우 공정성 모니터링이 모니터링되는 배치에 대해 추가 스코어링 요청을 작성합니다.
{: note}

{{site.data.keyword.aios_short}} 대시보드에서 시간이 경과함에 따른 모든 메트릭 값을 검토할 수 있습니다.

![설정된 임계값 미만 드리프트를 보여주는 공정성 지표 차트](images/fairness_metrics_001.png)

선호 및 비선호 결과와 같은 관련된 세부사항을 검토할 수 있습니다.

![공정성 세부사항](images/fairness_metrics_002.png)

트랜잭션 세부사항을 볼 수 있습니다.

![트랜잭션 목록을 보여주는 공정성 차트](images/fairness_metrics_003.png)

권장되는 편향성 제거된 스코어링 엔드포인트를 볼 수 있습니다.

![편향성 제거된 스코어링 엔드포인트의 세부사항](images/fairness_metrics_004.png)

### 지원되는 공정성 메트릭
{: #anlz_metrics_supfairmets}

다음 공정성 메트릭이 {{site.data.keyword.aios_short}}에서 지원됩니다.

- [그룹에 대한 공정성](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

{{site.data.keyword.aios_short}}에서 지원되는 보호된 속성은 다음과 같습니다. 

- [성별](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [인종](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [결혼 여부](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [연령](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [우편번호](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### 지원되는 공정성 세부사항
{: #anlz_metrics_supfairdets}

공정성 메트릭의 다음 세부사항이 {{site.data.keyword.aios_short}}에서 지원됩니다.

- 각 그룹에 대한 선호 백분율
- 모든 공정성 그룹에 대한 공정성 평균

```
                          (모니터 대상 그룹의 선호 결과 비율(%))
차별적 효과 비율 =  ____________________________________________
                          (참조 그룹의 선호 결과 비율(%))
```

- 모니터링된 각 그룹에 대한 데이터의 분포
- 페이로드 데이터의 분포
