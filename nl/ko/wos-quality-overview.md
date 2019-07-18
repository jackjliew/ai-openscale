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

# 품질 메트릭 개요 ![베타 태그](images/beta.png)
{: #anlz_metrics}

품질 모니터링을 사용하여 모델이 결과를 얼마나 잘 예측하는지 판별할 수 있습니다. 품질 모니터링이 사용으로 설정된 경우 기본적으로 1시간마다 메트릭 세트를 생성합니다. 필요한 경우 **품질 지금 확인** 단추를 클릭하거나 Python 클라이언트를 사용하여 이러한 메트릭을 생성할 수 있습니다.

품질 메트릭스는 다음 정보를 기반으로 계산됩니다.

- 수동으로 레이블이 지정된 피드백 데이터
- 이러한 데이터에 대한 모니터링된 배치 응답

적합한 모니터링을 위해 피드백 데이터를 정기적으로 {{site.data.keyword.aios_short}}에 기록해야 합니다. "피드백 데이터 추가" 옵션을 사용하거나 Python 클라이언트 또는 REST API를 사용하여 피드백 데이터를 제공할 수 있습니다.

Microsoft Azure ML Studio, Microsoft Azure ML 서비스 또는 Amazon Sagemaker ML 등의 {{site.data.keyword.aios_short}} 이외의 기계 학습 엔진의 경우 품질 모니터링에서는 모니터링된 배치에 대해 추가적인 스코어링 요청을 작성합니다.
{: note}

{{site.data.keyword.aios_short}} 대시보드에서 시간이 경과함에 따른 모든 메트릭 값을 검토할 수 있습니다.

![ROC 아래 영역의 드리프트를 보여주는 품질 메트릭 차트](images/quality_metrics_001.png)


일부 메트릭에 사용 가능한 2진 및 다중 클래스 분류에 대한 오차 행렬과 같은 관련 세부사항을 검토하려면, 차트를 클릭하십시오.

![품질 메트릭의 세부사항 테이블](images/quality_metrics_002.png)

## 지원되는 품질 메트릭
{: #anlz_metrics_supqualdets}

다음 품질 메트릭이 {{site.data.keyword.aios_short}}에서 지원됩니다.

- [ROC 아래 영역](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [PR 아래 영역](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [정확성](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [참 양성 비율(TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [거짓 양성 비율(FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [재현율](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [정밀도](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [F1 수치](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [로그 손실](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## 지원되는 품질 세부사항
{: #anlz_metrics_supqualdets_suppr_dets}

품질 메트릭에 대한 다음 세부사항이 {{site.data.keyword.aios_short}}에서 지원됩니다.

### 오차 행렬
{: #anlz_metrics_supqualdets_confusion-quickovr}

오차 행렬은 모니터링된 배치 응답에 대한 어느 피드백 데이터가 올바른지 또는 올바르지 않은지를 이해하는 데 도움을 줍니다.

자세한 정보는 [오차 행렬](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx)을 참조하십시오.
