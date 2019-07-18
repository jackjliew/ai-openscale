---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: dashboard, navigating, navigation, insights

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

# {{site.data.keyword.aios_short}} 살펴보기
{: #io-ov}

{{site.data.keyword.aios_full}} 대시보드를 통해 모니터링하고 있는 모든 배치를 추적할 수 있습니다. 대시보드는 {{site.data.keyword.aios_short}}에 대한 기본 보기로서, 대시보드를 통해 모델의 작업 수행 방식을 살펴볼 수 있습니다.
{: shortdesc}

## 인사이트
{: #io-ins}

**인사이트** 탭(![인사이트 대시보드](images/insight-dash-tab.png))은 배치 모니터링의 상위 레벨 보기를 제공합니다.

  ![인사이트 대시보드](images/insight-dashboard.png)

- ***모니터링되는 배치*** - 이 예에서 총 10개의 배치가 모니터됩니다. 10개의 다음 배치 중 8개가 개별 타일로 표시됩니다.

- ***정확성 경보*** - 총 3개의 정확성 경보가 다음 타일에 표시됩니다. 이 예에서, `Driver Performance`, `Market Analytics` 및 `Pricing Risk` 배치의 정확성 값이 각각 `60%`, `65%`, 및 `79%` 로 표시됩니다.

- ***공정성 경보*** - 총 6개의 공정성 경보가 있으며 작은 `BIAS` 태그로 아래 타일에 표시됩니다. 이 예에서 `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` 및 `Damage Cost Estimator` 배치의 공정성 값이 각각 `59%`, `68%`, `62%`, `64%`, `79%`, 및 `63%` 로 표시됩니다.

각 타일이 해당 배치에 대한 모니터링 활동의 요약을 제공합니다. `Call Center Routing` 배치 타일은 매우 안정적이며 정확한 모델을 표시하며 문제가 있어 보이지 않습니다.

### 다음 단계
{: #io-next}

개별 배치 타일 중 하나를 선택하여 해당 배치에 대한 세부사항을 볼 수 있습니다. 자세한 정보는 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-it-ov) 및 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.



## 트랜잭션
{: #io-tran}

**트랜잭션 설명** 탭(![트랜잭션 설명 탭](images/insight-transact-tab.png))을 사용하여 특정 배치 트랜잭션을 설명할 수 있는 특정 트랜잭션 ID를 검색하십시오. 자세한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.


