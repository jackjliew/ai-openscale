---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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


# 신뢰도별 예측 ![베타 태그](images/beta.png)
{: #anlz_metrics_payload-confidence}

각 클래스의 예측 클래스와 신뢰도 분포를 검토하여 선택한 데이터 범위에 있는 배치로 전송되는 스코어링 페이로드를 분석할 수 있습니다.
{: shortdesc}

   ![신뢰도 분포를 기준으로 예측을 맵핑하는 차트](images/by_confidence.png)
