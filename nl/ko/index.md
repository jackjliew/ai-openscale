---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 정보
{: #in-ov}

{{site.data.keyword.aios_full}}는 AI가 결합된 애플리케이션을 위한 엔터프라이즈 등급의 환경이며 비즈니스 범위에서 AI가 빌드되고 사용되는 방법을 시각화하며 투자에 대한 수익을 전달합니다.
{: shortdesc}

<p>&nbsp;</p>

## 구현
{: #in-imp}

다음은 {{site.data.keyword.aios_short}}을 구현하는 방법입니다.

- **{{site.data.keyword.aios_short}}** 구성: 사용하기 쉬운 그래픽 환경을 사용하여 AI 모델 및 배치가 저장되는 [페이로드 로깅 데이터베이스](/docs/services/ai-openscale?topic=ai-openscale-connect-db) 및 [Watson 기계 학습 인스턴스](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)를 설정하십시오.

- **모니터에 대한 작업**: 각 배치에 대해 {{site.data.keyword.aios_short}}기 해당 배치를 모니터할 방법을 구성하십시오. 다음을 모니터할 수 있습니다.

    - [공정성](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [정확성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)

- **모니터되는 데이터 보기 및 편집**: {{site.data.keyword.aios_short}} [대시보드](/docs/services/ai-openscale?topic=ai-openscale-io-ov)를 사용하면 쉽게 핵심 인사이트를 보고 배치의 문제를 식별할 수 있습니다. 모니터되는 각 특성에 대한 개별 데이터 점의 시각화는 추가 세부사항을 제공합니다.

<p>&nbsp;</p>

## 제한사항
{: #in-lim}

- 현재 릴리스는 하나의 데이터베이스, 하나의 Watson 기계 학습 인스턴스 및 하나의 {{site.data.keyword.aios_short}} 인스턴스만 지원합니다.

- 데이터베이스 및 Watson 기계 학습 인스턴스가 동일한 {{site.data.keyword.cloud_notm}} 계정에 배치되어야 합니다.

- Lite(무료) 플랜은 다음과 같은 월별 한계가 있습니다.

    - 두 개의 배치된 모델이 모니터링됨
    - 20개의 트랜잭션이 설명됨
    - 50,000개의 페이로드 레코드(누적)
    - 50,000개의 피드백 레코드(누적)

- {{site.data.keyword.aios_short}}은 PostgreSQL 또는 Db2 데이터베이스를 사용하여 모델 배치 출력 및 재교육 데이터를 저장합니다. Lite Db2 플랜은 현재 지원되지 않습니다.

- {{site.data.keyword.aios_short}}의 인스턴스당 20개의 배치된 모델이라는 라이센스 한계가 있습니다.

- 현재, 1MB보다 더 큰 이미지에 대해 설명을 생성할 수 없습니다.

<p>&nbsp;</p>

## 지원되는 모델 유형
{: #in-mod}

표 1. 모델 지원 세부사항

| 알고리즘 | **공정성** | **자동-편향성 제거** | **설명** | **정확성** |
|:---|:---:|:---:|:---:|:---:|
| **정형 분류** |예 | 예<sup>1</sup> |예 |예 |
| **정형 회귀**     |예 |아니오 |예 |예 |
| **텍스트 분류**       |아니오 |아니오 |예 |아니오 |
| **이미지 분류**      |아니오 |아니오 |예 |아니오 ||
{: caption="모델 지원 세부사항" caption-side="top"}

<sup>1</sup> 모델/프레임워크가 예측 확률을 출력하는 경우

<p>&nbsp;</p>

## 지원되는 기계 학습 엔진 및 프레임워크
{: #in-fram}

{{site.data.keyword.aios_short}} 서비스는 다음과 같은 기계 학습 엔진을 지원합니다. 각 런타임은 [지원되는 모델 유형](#in-mod) 목록에서 설명된 대로 다음 프레임워크에서 작성된 모델을 지원합니다.

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [사용자 정의](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS(ICP 전용)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

전체 지원에는 특정 프레임워크, 문제점 및 데이터 유형에 대한 다음 특성이 포함됩니다.

- 페이로드 로깅	
- 피드백 로깅	
- 성과 정확성	
- 런타임 편향성 발견	
- 설명 가능성	
- 자동 편향성 제거

<p>&nbsp;</p>

## 브라우저 지원
{: #in-brw}

{{site.data.keyword.aios_short}} 서비스 도구 사용에는 {{site.data.keyword.cloud_notm}}에서 요구하는 대로 동일한 레벨의 브라우저 소프트웨어가 필요합니다. 세부사항은 {{site.data.keyword.cloud_notm}} [필수 소프트웨어](/docs/overview?topic=overview-prereqs-platform#browsers-platform) 주제를 참조하십시오.

<p>&nbsp;</p>

## ModelOps CLI 도구
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI 모델 조작 도구 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window}를 사용하면 기계 학습 모델의 라이프사이클 관리와 연관된 태스크를 실행할 수 있습니다. 이 도구는 {{site.data.keyword.cloud_notm}} CLI 도구를 보완하며 [기계 학습 플러그인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}을 사용하여 보강됩니다.

<p>&nbsp;</p>

## Python 클라이언트
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 클라이언트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://ai-openscale-python-client.mybluemix.net/){: new_window}는 {{site.data.keyword.cloud_notm}}에 대해 {{site.data.keyword.aios_short}} 서비스를 사용하여 직접 작업하도록 해주는 Python 라이브러리입니다. {{site.data.keyword.aios_short}} 클라이언트 UI 대신 Python 클라이언트를 사용하여 직접 로깅 데이터베이스를 구성하고 기계 학습 엔진을 바인드하고 배치를 선택 및 모니터할 수 있습니다. 이런 방법으로 Python 클라이언트를 사용하는 예를 보려면 [{{site.data.keyword.aios_short}} sample Notebooks ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)를 참조하십시오.

<p>&nbsp;</p>

## 다음 단계
{: #in-next}

- 서비스 [시작하기](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- [API 참조 자료 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/ai-openscale){: new_window}를 참조하십시오.

다른 질문이 있으십니까? [IBM에 문의하십시오 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
