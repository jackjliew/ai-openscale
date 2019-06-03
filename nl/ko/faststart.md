---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 자동화된 설정
{: #wos-fast-start}

{{site.data.keyword.aios_short}}에서 모델을 모니터하는 방법을 빠르게 확인하려면 {{site.data.keyword.aios_short}} UI에 처음 로그인할 때 제공되는 데모 시나리오 옵션을 실행하십시오.  [UI 데모에 대한 작업](#wos-work-demo)을 참조하십시오.
{: shortdesc}

## 시작하기 전에
{: #wos-prereqs}

둘러보기를 시작하기 전에 다음 리소스가 이미 설정되어 있어야 합니다.

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## UI 데모에 대한 작업
{: #wos-work-demo}

1.  {{site.data.keyword.bluemix_full}}의 {{site.data.keyword.aios_short}} 인스턴스에 로그인하십시오.
1.  데모 시나리오에 대해 작업하려면 **데모 실행**을 클릭하십시오.

   ![데모 시작](images/fastpath_demo_11.31.04.png)

   {{site.data.keyword.aios_short}} 서비스가 프로비저닝되면 데모 시나리오를 검토할 수 있습니다.

   ![데모 미리보기](images/fastpath_demo_11.31.58.png)

프로비저닝이 완료되면 **시작합니다** 단추를 클릭하여 {{site.data.keyword.aios_short}} 대시보드를 둘러보고 [{{site.data.keyword.aios_short}}에서 결과 보기](#wos-open)를 진행하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.33.45.png)


## {{site.data.keyword.aios_short}}에서 결과 보기
{: #wos-open}

모델의 공정성 및 정확성에 대한 인사이트, 모니터링하는 데이터의 세부사항 및 개별 트랜잭션에 대한 설명 가능성을 확인하려면 {{site.data.keyword.aios_short}} 대시보드를 여십시오. 각 배치는 타일식으로 표시됩니다. 둘러보기는 다음 화면 캡처에 표시된 대로 `GermanCreditRiskModel`이라는 배치를 구성한 경우입니다.


   ![데모를 시작합니다](images/fastpath_demo_11.33.54.png)


### 인사이트 보기
{: #wos-insights}

인사이트 페이지에서는 구성되는 임계값에 의해 판별되는 공정성 및 정확성에 관한 문제를 한 눈에 볼 수 있습니다.

   ![데모를 시작합니다](images/fastpath_demo_11.34.00.png)

### 모니터링 데이터 보기
{: #wos-monitoring}

1.  인사이트 페이지에서 `GermanCreditRiskModelICP` 타일을 클릭하여 모니터링한 데이터의 세부사항을 확인하십시오.
1.  차트에서 마커를 클릭한 후 끌어서 데이터를 표시하는 일 및 기간을 확인한 다음 **세부사항 보기** 링크를 클릭하십시오. 또는 차트에서 다른 기간을 클릭하여 표시되는 데이터를 변경할 수 있습니다.

     - 예를 들면, 다음 화면은 특정 날짜 및 시간에 대한 데이터를 표시합니다. 날짜 및 시간은 언제 모듈을 실행하는지에 따라서 다릅니다.

     - 시계열 차트를 해석하는 것에 대한 정보는 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)을 참조하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.34.17.png)

1.  `SEX` 데이터 모니터링에 대한 세부사항을 보려면 드롭 다운 메뉴에서 `SEX`가 선택되었는지 확인하십시오.

    - 다음 화면 캡처에는 편향성이 있다는 점에 주의하십시오.
    
   ![데모를 시작합니다](images/fastpath_demo_11.34.27.png)

    - 특정 시간에 데이터 점 차트의 해석에 대한 정보는 [데이터 시각화](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual)를 참조하십시오.


### 설명 가능성 보기
{: #wos-explain}

이전 섹션에 표시된 시각화 화면에서, 주어진 기간에 대한 편향성이 존재하는 시기에 기여하는 요인을 이해하려면 **편향된 트랜잭션** 단일 선택 단추를 클릭하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.35.06.png)

지난 시간 동안의 트랜잭션 ID가 편향성이 있는 해당 트랜잭션에 대해 나열됩니다. 이 모듈에서 사용되는 모델의 경우 사용 가능한 요청에 대한 편향성이 있습니다.

   ![데모를 시작합니다](images/fastpath_demo_11.35.12.png)

트랜잭션을 발견하고 설명하는 것에 대한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)을 참조하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.35.50.png)

## 둘러보기 끝내기
{: #wos-done-demo}

1. **완료** 단추를 클릭하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.37.22.png)

2. **시작합니다** 단추를 클릭하여 {{site.data.keyword.aios_short}}에 대한 작업을 시작하십시오.

   ![데모를 시작합니다](images/fastpath_demo_11.33.45.png)


## 관련 정보
{: #wos-info}

- 편향성에 대한 자세한 내용은 [공정성](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)을 참조하십시오.
- 모델이 결과를 얼마나 잘 예상하는지에 대한 자세한 내용은 [정확성](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)을 참조하십시오.
- 차트, 데이터 및 트랜잭션 해석에 대해 알아보려면 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)을 참조하십시오.
