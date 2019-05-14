---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

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

# 새로운 기능
{: #rn-relnotes}

이 문서는 {{site.data.keyword.aios_full_notm}}의 새 기능 및 알려진 문제점에 대해 간략하게 설명합니다.
{: shortdesc}

## 2019년 3월 5일
{: #rn-5March2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

### 새로운 기능 및 변경사항
{: #rn-5March2019nf}

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*새 신용 위험 모델*__: 모든 스코어링 엔진에 대해 새 신용 위험 모델 예제와 튜토리얼이 지원됩니다. 자세한 정보는 [시작하기](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) 및 [추가 리소스](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov) 주제를 참조하십시오.

- __*편향성 제거 계산*__: {{site.data.keyword.aios_short}}에 의해 작성된 편향성 제거된 모델 및 프로덕션 모델 간을 토글할 수 있습니다. 자세한 정보는 [프로덕션 모델 및 편향성 제거된 모델](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) 및 [편향성 제거 작업 이해](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)를 참조하십시오.

## 2019년 2월 22일
{: #rn-22February2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

### 새로운 기능 및 변경사항
{: #rn-22February2019nf}

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*UI 업데이트*__: JSON 파일을 가져와서 구독을 작성하는 동안 프로그래밍 방식으로 모든 모니터와 기능을 구성할 수 있습니다. 또한 구성 파일을 내보낼 수 있습니다. 자세한 정보는 [JSON 파일을 사용하여 배치 구독 구성](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) 주제를 참조하십시오.

## 2019년 2월 7일
{: #rn-7February2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

### 새로운 기능 및 변경사항
{: #rn-7February2019nf}

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*UI 업데이트*__: [요청 시 공정성 및 정확성을 검사](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)할 수 있는 방법 및 [공정성 세부사항 차트](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)에서 트랜잭션 목록을 볼 수 있는 기능을 포함하여 {{site.data.keyword.aios_short}} 사용자 인터페이스가 몇 가지 개선되었습니다.

- __*설명 가능성 개선*__: 이제 모든 수가 PP(Pertinent Positive) 및 PN(Pertinent Negative) 값에 걸쳐 동일한 정밀도/배율을 갖습니다.

- __*Db2 SSL 지원*__: {{site.data.keyword.aios_short}}이 DB2 인증 정보를 사용하여 자체 서명된 인증서(Base-64 인코딩)를 전달하는 것을 지원합니다.

- __*IBM Cloud 데이터베이스 지원*__: {{site.data.keyword.aios_short}}에서 이제 Compose for PostgreSQL 및 Db2 뿐만 아니라 Databases for PostgreSQL도 지원합니다.

### 알려진 문제
{: #rn-7February2019ki}

- **사용자 정의 ML 서비스 인스턴스**

    - [Python 모듈](/docs/services/ai-openscale?topic=ai-openscale-as-module)에서 현재 사용자 정의 서비스 인스턴스에 대해 설명 가능성이 작동하지 않습니다. 이는 사용자 정의 서비스 인스턴스가 모듈 스크립트에 포함되지 않은 응답 데이터 내의 숫자 예측을 요구하기 때문입니다.

## 2018년 12월 14일
{: #rn-14December2018}

서비스에 대해 다음과 같은 새로운 기능과 변경사항이 사용 가능하며 알려진 문제점이 있습니다.

### 새로운 기능 및 변경사항
{: #rn-12nf}

베타 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*GA(General Availability)*__: IBM Cloud 표준(유료) 플랜으로서의 {{site.data.keyword.aios_full_notm}}의 GA(General Availability) 릴리스

- __*IBM Cloud Private for Data V1.2*__: {{site.data.keyword.aios_short}}을 IBM Cloud Private for Data V1.2에서 사용하는 경우, [설치 체크리스트](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)에서 설치 지침을 포함한 문서를 참조하십시오.

- __*모델 유형에 대한 지원*__: {{site.data.keyword.aios_short}}은 Watson 기계 학습에서의 AI 모델 배치 외에 Microsoft Azure, Amazon SageMaker 및 사용자 정의 환경에서의 모델 배치를 지원합니다. 자세한 정보는 [지원되는 모델 유형](/docs/services/ai-openscale?topic=ai-openscale-in-ov)을 참조하십시오.

- __*무료 "Lite" 데이터베이스*__: 무료 "Lite" 관리 데이터베이스는 {{site.data.keyword.aios_short}} 사용에 필요한 모든 것을 제공합니다. 세부사항은 [{{site.data.keyword.aios_short}} 가격 플랜 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/watson-openscale){: new_window}을 참조하십시오.

- __*편향성 모니터링*__: `float` 및 `double` 유형의 보호되는 속성을 지원하며 선형 회귀 모델에서 편향성 발견을 지원합니다. 또한 {{site.data.keyword.aios_short}}이 자동으로 사용자의 AI 모델의 편향성을 제거할 수 있습니다. 자세한 정보는 [공정성 이해](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)를 참조하십시오.

- __*설명 가능성*__: 회귀 모델, Python 함수 및 보완적인 대조 설명을 지원합니다. 자세한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.

- __*데이터 저장소*__: Watson 기계 학습에 의존하지 않는 품질 모니터링이며 Db2, Postgres 또는 Db2 on Cloud인지에 상관없이 자체 데이터베이스를 사용할 수 있는 기능입니다.

- __*NeuNetS(베타)*__: IBM Neural Network Synthesizer(NeuNetS)가 베타 릴리스로 사용 가능합니다(퍼블릭 클라우드 전용). 자세한 정보는 [NeuNetS 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}를 참조하십시오.

- __*강화된 UI*__: {{site.data.keyword.aios_short}} UI가 교육 데이터, 모델 ID 및 버전화, 히스토그램의 트랜잭션 ID 테이블에 대한 토글이 있는 런타임 히스토그램 분포를 포함하도록 강화되었습니다. 자세한 정보는 [특정 시간에 대한 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)를 참조하십시오.

- __*대체 튜토리얼 설정 옵션*__: 필수 IBM Cloud 서비스의 프로비저닝 및 구성을 자동화하고 샘플 데이터를 포함하여 IBM {{site.data.keyword.aios_full}} 애플리케이션을 보려면 Python 모듈을 설치하고 실행하십시오. [Python 모듈을 설치하여 {{site.data.keyword.aios_short}} 설정](/docs/services/ai-openscale?topic=ai-openscale-as-module)을 참조하십시오.

### 알려진 문제
{: #rn-12ki}

- **Microsoft Azure**

    - 두 가지 유형의 Azure 기계 학습 웹 서비스 중에서 `신규` 유형만 {{site.data.keyword.aios_short}}에 의해 지원됩니다. `일반` 유형은 지원되지 않습니다.

    - __*기본 입력 이름이 사용되어야 함*__: Azure 웹 서비스에서 기본 입력 이름은 `"input1"`입니다. 현재 이 필드는 {{site.data.keyword.aios_short}}에 필수이며 누락되는 경우 {{site.data.keyword.aios_short}}이 작동하지 않습니다.

      Azure 웹 서비스가 기본 이름을 사용하지 않는 경우, 입력 필드 이름을 `"input1"`로 변경하면 코드가 작동합니다.

- **AWS SageMaker**

    - __*BlazingText 알고리즘이 지원되지 않음*__: AWS SageMaker BlazingText 알고리즘 입력 페이로드 형식이 현재 {{site.data.keyword.aios_short}} 릴리스에서 지원되지 않습니다.

## 2018년 9월 17일
{: #rn-17September2018}

### 새로운 기능 및 변경사항
{: #rn-17nf}

- **베타 미리보기 릴리스** - {{site.data.keyword.aios_full_notm}}의 베타 미리보기 릴리스 사용을 환영합니다.
