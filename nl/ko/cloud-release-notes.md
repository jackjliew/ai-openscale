---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: release notes, what's new 

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

# 새로운 기능
{: #rn-relnotes}

이 문서는 {{site.data.keyword.aios_full_notm}}의 새 기능에 대해 간략하게 설명합니다.
{: shortdesc}

## 2019년 7월 9일
{: #rn-9jul2019}

다음과 같은 {{site.data.keyword.aios_short}}의 새로운 기능 및 변경사항이 제공됩니다.

- __*업데이트 및 확장된 온라인 도움말*__: {{site.data.keyword.aios_short}} 온라인 도움말은 컨텐츠 분할창을 사용한 주제 찾기가 보다 쉽도록 최근에 재구성되었습니다. 또한 많은 새 주제가 작성되고 확장되었습니다. 

   자세한 정보는 [인사이트 확보](/docs/services/ai-openscale?topic=ai-openscale-io-ov) 및 [Lite에서 유료 플랜으로 {{site.data.keyword.aios_short}} 업데이트](/docs/services/ai-openscale?topic=ai-openscale-cf-upgrade)를 참조하십시오. 
   
## 2019년 7월 2일
{: #rn-2jul2019}

다음과 같은 {{site.data.keyword.aios_short}}의 새로운 기능 및 변경사항이 제공됩니다.

- __*드리프트 발견*__: ![베타 태그](images/beta.png)

  {{site.data.keyword.aios_short}}은 이제 드리프트 발견을 지원합니다.

   자세한 정보는 [드리프트 발견](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)을 참조하십시오.

- __*Microsoft Azure ML 서비스 지원*__: {{site.data.keyword.aios_short}}은 이제 Azure ML 서비스 AI 모델과 {{site.data.keyword.aios_short}}의 공정성, 정확성 및 설명 가능성을 통합하는 방법을 제공하는 Microsoft Azure ML 서비스를 지원합니다.

   자세한 정보는 [Microsoft Azure ML 서비스 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)를 참조하십시오.

- __*개선된 워크플로우*__: {{site.data.keyword.aios_short}}은 더 적은 수의 클릭과 더 많은 설명 가능성을 통해 작업을 빠르게 수행할 수 있도록 워크플로우를 개선하기 위해 열심히 노력해 왔습니다. 탐색 패널을 사용하면 사용자의 위치를 확인하고 구성 태스크 사이에서 앞뒤로 쉽게 이동할 수 있습니다.

   자세한 정보는 [배치를 위해 모니터 준비](/docs/services/ai-openscale?topic=ai-openscale-mo-config)를 참조하십시오.

- __*복수의 기계 학습 제공자*__: 하나의 기계 학습 제공자 또는 엔진에 묶여 있을 이유가 없습니다. {{site.data.keyword.aios_short}}의 새 버전을 사용하면 복수의 제공자를 추가하여 해당 제공자의 고유 기능을 활용하거나 레거시 앱에 지속성을 제공할 수 있습니다.

   자세한 정보는 [여러 기계 학습 엔진 지원](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)을 참조하십시오.

- __*더 많은 즉시 사용 가능한 메트릭*__: {{site.data.keyword.aios_short}}이 이 버전을 사용하면 많은 새 공정성, 품질, 동작, 성능 및 분석 메트릭이 제공됩니다. 더 큰 상자가 필요합니다!

   자세한 정보를 보려면 [품질 메트릭 개요](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)를 참조한 후 주위를 클릭하여 [공정성](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness), [성능](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through), [분석](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload) 및 [동작](/docs/services/ai-openscale?topic=ai-openscale-behavior-ovr)으로 이동하십시오.

- __*편향성을 따라 가속화*__: 편향성 구성에 대해 제안된 공정성 속성 및 자동 값을 사용하면 {{site.data.keyword.aios_short}}이 배치된 모델에서 잠재적인 공정성 임계값 위반을 발견하는 위치를 쉽게 확인할 수 있습니다. 추천된 특성을 승인하거나 값을 변경하도록 선택할 수 있습니다.

   자세한 정보는 [공정성 메트릭 개요](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)를 참조하십시오.

## 2019년 6월 11일
{: #rn-11June2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

- __*업데이트된 대시보드 기능*__: {{site.data.keyword.aios_short}} 대시보드를 여러 번 개정했습니다. 이 새 버전에는 다음과 같은 개선사항이 포함되어 있습니다.

    - 새로운 도움말 패널을 사용하면 StackOverflow, IBM 지원 센터 등의 리소스를 찾기가 쉬워짐 
    - 대시보드에서 다국어 지원 사용 가능
    - 사용 가능성 향상

## 2019년 6월 7일
{: #rn-7June2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

- __*향상된 명령행 인터페이스*__: 명령행 인터페이스인 ibm-ai-openscale-cli가 업데이트되었으며 이제 0.2.148이 릴리스되었습니다. 이 새 버전에는 다음과 같은 개선사항이 포함되어 있습니다.

    - OpenScale에서 지원하는 전체 범위의 새 품질 지표를 포함하도록 품질 지표 히스토리가 업데이트됨
    - IBM DB2를 사용할 때 직접 SSL 인증서를 지정하도록 지원
    - 새 ibm-ai-openscale 2.1.8 Python SDK 지원
    - 기타 버그 수정 및 안정성 개선

   `pip install -U ibm-ai-openscale-cli` 명령을 실행하여 PyPl에서 설치하고 `ibm-ai-openscale-cli --help` 명령을 실행하여 사용법 도움말을 가져오십시오. 자세한 정보는 [PyPI 프로젝트 페이지](https://pypi.org/project/ibm-ai-openscale-cli)를 참조하십시오.

## 2019년 5월 29일
{: #rn-29May2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

- __*편향성 시각화 개선사항*__: ![베타 태그](images/beta.png) 편향성 시각화에는 다음 보기가 포함됩니다. 

    - 페이로드 + 섭동됨: 평가에 필요한 최소 레코드 수가 충족되지 않은 경우 이전 시간의 추가 레코드 및 선택한 시간 동안 수신된 스코어링 요청을 포함합니다. 모니터 대상 기능의 값이 변경되는 경우 모델의 응답을 테스트하는 데 사용되는 추가적인 섭동된/합성된 레코드가 포함됩니다.
    - 페이로드: 선택한 시간 동안 모델에서 수신한 실제 스코어링 요청입니다.
    - 훈련: 모델을 훈련시키는 데 사용된 훈련 데이터 레코드입니다.
    - 편향성 제거됨: 런타임 및 섭동된 데이터를 처리한 후 편향성 제거 알고리즘의 출력입니다.

   자세한 정보는 [편향성 시각화](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz)를 참조하십시오.

- __*편향성 제거된 출력의 정확도 계산*__: 정확도 계산에는 편향성 제거된 출력이 포함됩니다. 편향성 제거된 모델의 정확도를 프로덕션 모델의 정확도와 비교할 수 있습니다.

   자세한 정보는 [정확성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view)을 참조하십시오.

- __*여러 기계 학습 엔진 지원*__: {{site.data.keyword.aios_short}}에서는 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820)를 통해 프로비저닝을 수행하는 경우 단일 인스턴스에서 여러 기계 학습 엔진을 지원합니다.

   자세한 정보는 [여러 기계 학습 엔진 지원](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)을 참조하십시오.

- __*국제화 지원*__: {{site.data.keyword.aios_short}}은 현지화된 버전을 지원하며 지원되는 언어의 처리 데이터를 포함합니다. {{site.data.keyword.aios_short}} 사용자 인터페이스, 문서 및 오류 메시지는 현재 다음 언어로 번역되어 있습니다. 
    - 독일어
    - 프랑스어
    - 이태리어
    - 스페인어
    - 브라질 포르투갈어
    - 일반어
    - 중국어
    - 대만어
    - 한국어

   자세한 정보(제한사항 포함)는 [{{site.data.keyword.aios_short}}의 지원 언어](/docs/services/ai-openscale?topic=ai-openscale-sl-langs)를 참조하십시오.

- __*{{site.data.keyword.pm_full}} 프레임워크 개선사항*__: {{site.data.keyword.aios_short}}은 이제 {{site.data.keyword.pm_full}} 엔진에서 scikit-learn 및 XGBoost 프레임워크를 지원합니다.

   자세한 정보는 [{{site.data.keyword.pm_full}} 프레임워크](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml)를 참조하십시오.

## 2019년 4월 25일
{: #rn-25April2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

가용성 개선 및 보안 업데이트 외에 IBM 개발자는 새로운 기능으로 항상 바쁘게 작업하고 있습니다. 이전 몇 주에 걸쳐 추가되거나 개선된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*자동화된 설정 둘러보기*__: {{site.data.keyword.aios_short}} 환경을 설정하는 새로운 둘러보기 기반 방법. [자동화된 설정](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)을 사용하여 서비스를 프로비저닝하고 모델을 다운로드하여 구성하십시오. {{site.data.keyword.aios_short}}의 새 인스턴스가 있는 경우에 이 옵션을 사용할 수 있습니다.
- __*베타로 전환*__: ![베타 태그](images/beta.png) 새 토글 **새 베타 버전 탐색**을 통해 베타 환경에서 작업할 수 있으며 여기에서 모든 최신 기능 및 새 기능을 확인할 수 있습니다. 표시되는 것이 맘에 들지 않습니까? **원래 버전으로 돌아가기**를 클릭하여 다시 전환할 수 있습니다. 구성과 모니터는 영향을 받지 않습니다. 다음 기능은 현재 베타 프로그램의 일부입니다.
    - __*오차 행렬*__: [오차 행렬은](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx) 거짓 양성 및 거짓 음성을 표시합니다. 피드백 레코드의 서브세트를 보려면 셀을 클릭하십시오.

## 2019년 4월 10일
{: #rn-10April2019}

- __*Express Path 도구가 이제 고객 모델을 지원함*__: {{site.data.keyword.aios_short}}에 대한 온보딩 프로세스를 자동화합니다.

   자세한 정보는 [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/)를 참조하십시오.


## 2019년 3월 5일
{: #rn-5March2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*새 신용 위험 모델*__: 모든 스코어링 엔진에 대해 새 신용 위험 모델 예제와 튜토리얼이 지원됩니다. 자세한 정보는 [시작하기](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) 및 [추가 리소스](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov) 주제를 참조하십시오.

- __*편향성 제거 계산*__: {{site.data.keyword.aios_short}}에 의해 작성된 편향성 제거된 모델 및 프로덕션 모델 간을 토글할 수 있습니다. 자세한 정보는 [프로덕션 모델 및 편향성 제거된 모델](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) 및 [편향성 제거 작업 이해](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)를 참조하십시오.

## 2019년 2월 22일
{: #rn-22February2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*UI 업데이트*__: JSON 파일을 가져와서 구독을 작성하는 동안 프로그래밍 방식으로 모든 모니터와 기능을 구성할 수 있습니다. 또한 구성 파일을 내보낼 수 있습니다. 자세한 정보는 [JSON 파일을 사용하여 배치 구독 구성](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) 주제를 참조하십시오.

## 2019년 2월 7일
{: #rn-7February2019}

다음과 같은 새로운 기능과 서비스의 변경사항이 사용 가능합니다.

이전 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*UI 업데이트*__: [요청 시 공정성 및 정확성을 검사](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)할 수 있는 방법 및 [공정성 세부사항 차트](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)에서 트랜잭션 목록을 볼 수 있는 기능을 포함하여 {{site.data.keyword.aios_short}} 사용자 인터페이스가 몇 가지 개선되었습니다.

- __*설명 가능성 개선*__: 이제 모든 수가 PP(Pertinent Positive) 및 PN(Pertinent Negative) 값에 걸쳐 동일한 정밀도/배율을 갖습니다.

- __*Db2 SSL 지원*__: {{site.data.keyword.aios_short}}이 DB2 인증 정보를 사용하여 자체 서명된 인증서(Base-64 인코딩)를 전달하는 것을 지원합니다.

- __*{{site.data.keyword.Bluemix}} 데이터베이스 지원*__: {{site.data.keyword.aios_short}}에서 이제 Compose for PostgreSQL 및 Db2 뿐만 아니라 Databases for PostgreSQL도 지원합니다.

## 2018년 12월 14일
{: #rn-14December2018}

서비스에 대해 다음과 같은 새로운 기능과 변경사항이 사용 가능하며 알려진 문제점이 있습니다.

베타 릴리스 이후에 추가되거나 강화된 {{site.data.keyword.aios_short}} 기능은 다음과 같습니다.

- __*GA(General Availability)*__: {{site.data.keyword.Bluemix}} 표준(유료) 플랜으로서의 {{site.data.keyword.aios_full_notm}}의 GA(General Availability) 릴리스

- __*{{site.data.keyword.icp4dfull_notm}} V1.2*__: {{site.data.keyword.wos4d_full}} V1.2를 사용하는 경우 [설치 체크리스트](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#install)에서 설치 지시사항을 포함한 문서를 참조하십시오.

- __*모델 유형에 대한 지원*__: {{site.data.keyword.aios_short}}은 {{site.data.keyword.pm_full}}에서의 AI 모델 배치 외에 Microsoft Azure, Amazon SageMaker 및 사용자 정의 환경에서의 모델 배치를 지원합니다. 자세한 정보는 [지원되는 모델 유형](/docs/services/ai-openscale?topic=ai-openscale-in-ov)을 참조하십시오.

- __*무료 "Lite" 데이터베이스*__: 무료 "Lite" 관리 데이터베이스는 {{site.data.keyword.aios_short}} 사용에 필요한 모든 것을 제공합니다. 세부사항은 [{{site.data.keyword.aios_short}} 가격 플랜](https://{DomainName}/catalog/services/watson-openscale){: external}을 참조하십시오.

- __*편향성 모니터링*__: `float` 및 `double` 유형의 보호되는 속성을 지원하며 선형 회귀 모델에서 편향성 발견을 지원합니다. 또한 {{site.data.keyword.aios_short}}이 자동으로 사용자의 AI 모델의 편향성을 제거할 수 있습니다. 자세한 정보는 [공정성 이해](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)를 참조하십시오.

- __*설명 가능성*__: 회귀 모델, Python 함수 및 보완적인 대조 설명을 지원합니다. 자세한 정보는 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.

- __*데이터 저장소*__: {{site.data.keyword.pm_full}}에 의존하지 않는 품질 모니터링이며 Db2, Postgres 또는 Db2 on Cloud인지에 상관없이 자체 데이터베이스를 사용할 수 있는 기능입니다.

- __*강화된 UI*__: {{site.data.keyword.aios_short}} UI가 훈련 데이터, 모델 ID 및 버전화, 히스토그램의 트랜잭션 ID 테이블에 대한 토글이 있는 런타임 히스토그램 분포를 포함하도록 강화되었습니다. 자세한 정보는 [특정 시간에 대한 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)를 참조하십시오.

- __*대체 튜토리얼 설정 옵션*__: 필수 {{site.data.keyword.Bluemix}} 서비스의 프로비저닝 및 구성을 자동화하고 샘플 데이터를 포함하여 IBM {{site.data.keyword.aios_full}} 애플리케이션을 보려면 Python 모듈을 설치하고 실행하십시오. [Python 모듈을 설치하여 {{site.data.keyword.aios_short}} 설정](/docs/services/ai-openscale?topic=ai-openscale-as-module)을 참조하십시오.

## 2018년 9월 17일
{: #rn-17September2018}

- **베타 미리보기 릴리스** - {{site.data.keyword.aios_full_notm}}의 베타 미리보기 릴리스 사용을 환영합니다.

<p>&nbsp;</p>

## 다음 단계
{: #relnotes-in-next}

다른 질문이 있으십니까?

- [제한사항](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [알려진 문제](/docs/services/ai-openscale?topic=ai-openscale-rn-12ki#cloud-limitations)
