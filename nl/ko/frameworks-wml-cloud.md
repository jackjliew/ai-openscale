---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: supported frameworks, models, model types, limitations, limits

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# WML 프레임워크
{: #frmwrks-wml}

{{site.data.keyword.aios_full}}에서는 다음 {{site.data.keyword.pm_full}} 프레임워크를 전적으로 지원합니다. 
{: shortdesc}

표 1. 프레임워크 지원 세부사항

| 프레임워크 | 문제점 유형 | 데이터 유형 |
|:---|:---:|:---:|
| Apache Spark MLlib | 분류 | 정형 |
| Python 함수 | 분류 | 정형 |
| Python 함수 | 회귀 | 정형 |
| XGBoost | 분류 | 정형 |
| XGBoost | 회귀 | 정형 |
| scikit-learn | 분류 | 정형 |
| scikit-learn | 회귀 | 정형 |
| Keras with TensorFlow<sup>1</sup> | 분류 | 비정형(이미지, 텍스트) |
| Keras with TensorFlow<sup>1</sup> | 회귀 | 비정형(이미지, 텍스트) |
{: caption="프레임워크 지원 세부사항" caption-side="top"}

<sup>1</sup>Keras 지원에는 공정성에 대한 지원은 포함되지 않습니다.
{: note}



