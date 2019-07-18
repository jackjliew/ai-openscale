---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# 지원되는 기계 학습 엔진, 프레임워크 및 모델
{: #in-fram}

{{site.data.keyword.aios_short}} 서비스는 다음과 같은 기계 학습 엔진을 지원합니다. 각 런타임은 다음 프레임워크에서 작성되는 모델을 지원합니다.

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [Azure ML 서비스](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azureservice#frmwrks-azureservice)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [사용자 정의](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)({{site.data.keyword.wos4d_full}}에서만 사용 가능)

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

전체 지원에는 특정 프레임워크, 문제점 및 데이터 유형에 대한 다음 특성이 포함됩니다.

- 페이로드 로깅	
- 피드백 로깅	
- 성과 정확성	
- 런타임 편향성 발견	
- 설명 가능성	
- 자동 편향성 제거

<p>&nbsp;</p>


## 지원되는 모델 유형
{: #abt-models}

표 1. 모델 지원 세부사항

| 알고리즘 | **공정성** | **자동 편향성** | **설명** | **정확도** |
|:---|:---:|:---:|:---:|:---:|
| **구조화된 분류** | 예 | 예<sup>1</sup> | 예<sup>1</sup> | 예 |
| **구조화된 회귀**     | 예 | 제공 예정 | 예 | 예 |
| **텍스트 분류**       | 아니오 - 현재 연구 중인 주제 | 아니오 - 현재 연구 중인 주제 | 예<sup>1</sup> |아니오 |
| **이미지 분류**      | 아니오 - 현재 연구 중인 주제 | 아니오 - 현재 연구 중인 주제 | 예<sup>1</sup> |아니오 ||
{: caption="모델 지원 세부사항" caption-side="top"}

<sup>1</sup> 모델 / 프레임워크에서 예측 확률을 출력하는 경우

<p>&nbsp;</p>

## 브라우저 지원
{: #in-brw}

{{site.data.keyword.aios_short}} 서비스 도구 사용에는 {{site.data.keyword.cloud_notm}}에서 요구하는 대로 동일한 레벨의 브라우저 소프트웨어가 필요합니다. 세부사항은 {{site.data.keyword.cloud_notm}} [필수 소프트웨어](/docs/overview?topic=overview-prereqs-platform#browsers-platform) 주제를 참조하십시오.

<p>&nbsp;</p>

## ModelOps CLI 도구
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI 모델 조작 도구](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}를 사용하면 기계 학습 모델의 라이프사이클 관리와 연관된 태스크를 실행할 수 있습니다. 이 도구는 {{site.data.keyword.cloud_notm}} CLI 도구를 보완하며 [기계 학습 플러그인](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}을 사용하여 보강됩니다.

<p>&nbsp;</p>

## Python 클라이언트
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 클라이언트](http://ai-openscale-python-client.mybluemix.net/){: external}는 {{site.data.keyword.cloud_notm}}에서 {{site.data.keyword.aios_short}} 서비스를 사용하여 직접 작업할 수 있게 하는 Python 라이브러리입니다. {{site.data.keyword.aios_short}} 클라이언트 UI 대신 Python 클라이언트를 사용하여 직접 로깅 데이터베이스를 구성하고 기계 학습 엔진을 바인드하고 배치를 선택 및 모니터할 수 있습니다. 이 방법으로 Python 클라이언트를 사용하는 예를 보려면 [{{site.data.keyword.aios_short}} 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)을 참조하십시오.

<p>&nbsp;</p>

## 다음 단계
{: #in-next}

- [API 참조 자료](https://{DomainName}/apidocs/ai-openscale){: external}를 보십시오.

다른 질문이 있으십니까? 

- [새로운 기능](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM에 문의](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}하십시오.
