---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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
