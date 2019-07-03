---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# 오차 행렬 ![베타 태그](images/beta.png)
{: #it-conf-mtx}

품질 메트릭의 세부사항으로 모델이 잘못 분석한 레코드를 확인할 수 있습니다. 이러한 이상 항목은 2진 분류 모델에 대해 거짓 양성 또는 거짓 음성일 수 있으며 다중 클래스 모델에 대한 잘못된 클래스 지정일 수 있습니다. 또한 모델이 올바르게 분석하지 않은 피드백 레코드 목록도 볼 수 있습니다.
{: shortdesc}

일부 메트릭에 사용 가능한 2진 및 다중 클래스 분류에 대한 오차 행렬과 같은 관련 세부사항을 검토하려면, 차트를 클릭하십시오.

![품질 메트릭의 세부사항 테이블](images/quality_metrics_002.png)

## 단계
{: #it-conf-mtx-steps}

1. **품질** 차트(예: **정확성**)에서 시간/일을 클릭하십시오. 
    
    ![편향된 트랜잭션 목록](images/Confusion_Matrix_040819.004.png)

1. 오차 행렬은 거짓 양성 및 거짓 음성을 표시합니다. 피드백 레코드의 서브세트를 보려면 셀을 클릭하십시오.

    ![편향된 트랜잭션 목록](images/Confusion_Matrix_040819.005.png)

1. 피드백 레코드를 검토하고 피드백 레코드 분석 결과에 대해 설명을 요청하십시오.

    ![편향된 트랜잭션 목록](images/Confusion_Matrix_040819.006.png)

1. 트랜잭션이 인라인으로 표시됩니다.

    ![편향된 트랜잭션 목록](images/Confusion_Matrix_040819.007.png)

