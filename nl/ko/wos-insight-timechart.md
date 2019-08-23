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

# 배치에 대한 데이터 보기
{: #it-vdep}

배치에 대한 모니터링 데이터를 볼 대상 배치를 대시보드에서 선택하십시오. 표제에 **모델 ID** 및 **작성된 날짜** 필드 등의 배치된 모델에 대한 정보가 표시됩니다.
{: shortdesc}

![시계열 차트가 공정성 스코어 및 하루의 시간과 함께 표시됨](images/insight-time-chart.png)

알고리즘 검사는 매시간 실행되므로 요청 시 공정성 및 품질을 검사하기 위한 링크도 제공됩니다. **스케줄** 패널에서 다음과 같은 링크를 클릭하여 데이터에 대한 즉시 검사를 작성할 수 있습니다.

![공정성 확인 단추가 표시됨](images/wos-fairness-button.png)


![품질 확인 단추가 표시됨](images/wos-quality-button.png)

다음으로 차트를 클릭한 후 차트를 가로질러 마커를 이동하여 개별 시간에 대한 통계를 보십시오.

![세부사항을 보려면 클릭하라고 알려주는 도구 팁 및 선택된 차트의 특정 데이터 점과 함께 시계열 차트 세부사항이 표시됨](images/wos-insight-time-detail.png)

- ***공정성***: 두 개의 공정성 특성(성별 및 연령)이 승인을 위해 설정된 임계값을 충족했습니다.
- ***품질***: 구성된 임계값 내에 있지 않아 **ROC 아래 영역** 메트릭이 경보를 표시합니다.
- ***분단 평균 요청***: 분당 처리된 레코드 수를 보려면 **처리량** 메트릭을 클릭하십시오. 처리량은 매분마다 계산되고 한 시간 동안의 평균 값이 차트에서 보고됩니다.


## 트랜잭션 보기
{: #it-tra}

이 옵션을 사용하면 **트랜잭션 보기** 단추를 클릭할 때 편향성에 기여하는 개별 트랜잭션을 볼 수 있습니다.

![트랜잭션 보기 단추가 표시됨](images/view_transactions.png)

배치가 편향된 방법으로 작동한 트랜잭션의 목록이 나열됩니다. 설명 가능성 탭에서 트랜잭션에 대한 세부사항을 가져오려면 임의의 트랜잭션 ID에 대한 **설명** 링크를 클릭하십시오. 자세한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.

**모든 트랜잭션** 보기를 선택하여 선택된 특성(예: "AGE") 및 선택된 기간(예: "2018년 9월 15일 1:00 PM")의 모든 트랜잭션을 보십시오.

![트랜잭션이 특정 데이터 점의 모든 트랜잭션을 나열함](images/transaction_list1.png)

**편향된 트랜잭션** 보기를 선택하여 편향된 결과를 수신한 트랜잭션의 서브세트만 보십시오. 편향된 각 트랜잭션은  모니터되는 특성(AGE)의 값 변경이 어떻게 편향된 트랜잭션에 대해 선호 결과를 발생시키는지 보여주는 유사하나 약간 개조된(섭동) 트랜잭션과 비교됩니다.

![트랜잭션이 편향된 트랜잭션만 나열함](images/transaction_list2.png)


