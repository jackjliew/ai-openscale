---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# 스코어링 요청 전송
{: #cdb-score}

모니터를 구성하기 위해 {{site.data.keyword.aios_short}}은 모니터할 데이터의 로깅을 시작할 수 있도록 스코어링 페이로드의 전송을 요구합니다.

- {{site.data.keyword.pm_full}}에 배치된 모델의 경우 페이로드 로깅 API를 사용하거나 {{site.data.keyword.pm_full}}에서 배치된 모델을 배치하는 옵션이 있습니다. {{site.data.keyword.pm_short}}에서 스코어링되는 배치된 모델의 경우 {{site.data.keyword.aios_short}}에 자동으로 전송됩니다.  
- Microsoft Azure, Amazon SageMaker 등의 기타 기계 학습 엔진 또는 사용자 정의 기계 학습 엔진의 경우에는 페이로드 로깅 API를 사용하여 스코어링 페이로드를 전송해야 합니다. 자세한 정보는 [비{{site.data.keyword.pm_full}} 서비스 인스턴스의 페이로드 로깅](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)을 참조하십시오.

## 페이로드 로깅 단계
{: #cdb-score-apisteps}

1. 배치를 선택한 후 **페이로드 로깅** 페이지로 이동하십시오. 
2. `cURL` 또는 `Python` 탭을 클릭하여 `cURL` 또는 `Python` 코드를 사용할지 여부를 선택하십시오.
3. **클립보드에 복사**를 클릭한 후 붙여넣어 모델 배치 요청 및 응답 데이터를 로깅하십시오. 자세한 정보는 [비{{site.data.keyword.pm_full}} 서비스 인스턴스의 페이로드 로깅](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)을 참조하십시오.

코드 스니펫에 제공되는 필드 및 값은 예이므로 이를 사용자의 실제 값으로 대체해야 합니다.
{: important}

![데이터베이스 선택](images/config-send-scoring.png)

페이로드 로깅을 실행하고 나면 선택된 배치에 대한 **모니터 준비 완료** 열에 체크표시가 나타납니다. 계속하려면 **모니터 구성**을 클릭하십시오.

## 스코어링 요청 수 이해
{: #cdb-score-capacity}

스코어링 요청은 {{site.data.keyword.aios_short}} 처리의 중요한 부분입니다. 모델 스코어링을 위해 트랜잭션 레코드를 전송할 때마다 {{site.data.keyword.aios_short}} 서비스가 섭동을 수행하고 설명을 작성할 수 있도록 추가 처리가 생성됩니다.

- 표 형식, 텍스트, 이미지 모델의 경우 다음과 같은 기준선 요청이 데이터 점을 생성합니다.

   - 1개의 스코어링 요청이 5000개의 데이터 점을 생성합니다.

- 표 형식 분류 모델의 경우에만 대조 설명을 위해 추가 스코어링 요청이 작성됩니다. 선행 기준선 요청에 다음 요청이 추가됩니다.

   - 100개의 스코어링 요청은 요청당 51개의 추가 데이터 점을 생성합니다.
   - 101개의 스코어링 요청은 요청당 1개의 추가 데이터 점을 생성합니다.


## 다음 단계
{: #cdb-score-next-steps-scoringreq}

[모니터를 구성](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config)합니다.
