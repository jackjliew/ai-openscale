---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: Python, install, python module, setup, set up, insights, explainability

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

# Python 모듈을 설치하여 {{site.data.keyword.aios_short}} 설정
{: #as-module}

필수 {{site.data.keyword.cloud_notm}} 서비스의 프로비저닝 및 구성을 자동화하고 샘플 데이터를 포함하여 {{site.data.keyword.aios_full}} 애플리케이션을 보려면 Python 모듈을 설치하십시오.
{: shortdesc}

## 해당 모듈 정보
{: #as-about}

- 이 모듈은 숙련된 사용자가 [시작하기](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) 튜토리얼에서 설명한 대로 직접 서비스를 프로비저닝하고 구성할 필요 없이 실행 중인 {{site.data.keyword.aios_short}}의 인스턴스를 볼 수 있는 대체 방안을 제공합니다.
- Python 모듈은 사용자가 보유한 서비스를 확인하고 {{site.data.keyword.aios_short}} 등의 필수 서비스를 작성하는 프로세스를 런 스루합니다. 모듈이 실행된 후 {{site.data.keyword.cloud_notm}} 대시보드에서 {{site.data.keyword.aios_short}}을 시작하여 모델을 모니터링하는 방법을 볼 수 있습니다.

## 시작하기 전에
{: #as-prereqs}

1. [{{site.data.keyword.cloud_notm}} API 키를 작성하고 다운로드하십시오](/docs/iam?topic=iam-userapikey#create_user_key). 후속 단계에서 API 키를 입력해야 합니다.

2. [Python 3의 임의의 릴리스를 설치![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.python.org/downloads/){: new_window}하십시오.

  Python 3은 필수한 pip 패키지 관리 시스템을 포함합니다.
  {: note}

3. 다음 명령을 실행하여 `ibm-ai-openscale-cli` 패키지를 설치하십시오.

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    시스템에 pip 버전이 둘 이상 설치된 경우, `pip3 install -U ibm-ai-openscale-cli`에서와 같이 `pip` 대신 `pip3`를 실행해야 합니다.
    {: tip}

4. 기존 {{site.data.keyword.pm_short}} 서비스 인스턴스가 있는 경우, [{{site.data.keyword.cloud_notm}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "External 외부 링크 아이콘")](https://{DomainName}){: new_window}를 확인하여 서비스가 Cloud Foundry가 아니라 IAM({{site.data.keyword.iamshort}})에 의해 관리되는지 확인하십시오.

  **중요**: 모듈이 {{site.data.keyword.pm_short}}의 인스턴스를 확인합니다. 인스턴스가 있는 경우 모듈이 이를 사용합니다. 그러나 인스턴스가 Cloud Foundry에 의해 관리되는 경우, [모듈을 실행하기 전에 IAM 리소스 그룹으로 마이그레이션](/docs/resources?topic=resources-migrate#migrate)해야 합니다.

## 모듈 실행
{: #as-run}

다음 명령을 실행하십시오.

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## {{site.data.keyword.aios_short}}에서 결과 보기
{: #as-open}

모델의 공정성 및 정확성, 모니터되는 데이터의 세부사항 및 개별 트랜잭션에 대한 설명 가능성에 대한 인사이트를 보려면 [{{site.data.keyword.aios_short}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}를 여십시오.

- 샘플 데이터에 대한 시나리오를 이해하려면 [유스 케이스 및 {{site.data.keyword.aios_short}}의 값](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use)을 읽으십시오.

### 인사이트 보기
{: #as-insights}

[{{site.data.keyword.aios_short}} 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}에서 **인사이트** 탭을 클릭하면 배치된 모델에 대한 메트릭 개요가 표시됩니다. ![인사이트](images/insight-dash-tab.png)

- 인사이트 페이지에서는 구성되는 임계값에 의해 판별되는 공정성 및 정확성에 관한 문제를 한 눈에 볼 수 있습니다.

- 각 배치는 타일식으로 표시됩니다. 모듈은 다음 화면 캡처에서 보듯이 `GermanCreditRiskModel`이라는 배치로 구성됩니다.

  ![인사이트 개요](images/setup01-0206.png)

### 모니터링 데이터 보기
{: #as-monitoring}

1. Insights 페이지에서 `GermanCreditRiskModel` 타일을 클릭하여 모니터되는 데이터에 대한 세부사항을 보십시오.
2. 마커를 차트를 가로질러 밀어서 데이터를 표시하는 대상 일 및 시간을 확인하고 **데이터 표시** 링크를 클릭하십시오.

   - 예를 들면, 다음 화면은 특정 날짜 및 시간에 대한 데이터를 표시합니다. 날짜 및 시간은 언제 모듈을 실행하는지에 따라서 다릅니다.

   - 시계열 차트를 해석하는 것에 대한 정보는 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-it-ov)을 참조하십시오.

    ![모니터 데이터](images/setup02-0206.png)

3. `AGE` 데이터 모니터링에 대한 세부사항을 보려면 드롭 다운 메뉴에서 `AGE`가 선택되었는지 확인하십시오.

  - 다음 화면 캡처에서, 편향성이 없음을 확인하십시오.

  - 특정 시간에 데이터 점의 차트를 해석하는 것에 대한 정보는 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp)을 참조하십시오.

    ![세부사항 보기](images/setup03-0206.png)

### 설명 가능성 보기
{: #as-explain}

이전 절에서 표시된 시각화 화면에 지정된 기간에 대한 편향성이 있을 때 기여하는 요인을 이해하려면 **트랜잭션 보기** 단추를 선택하십시오.

지난 시간 동안의 트랜잭션 ID가 편향성이 있는 해당 트랜잭션에 대해 나열됩니다. 이 모듈에서 사용된 모델의 경우 사용 가능한 요청에 대한 편향성이 없습니다. 그러므로 다음 화면 캡처의 기간 동안 트랜잭션이 표시되지 않습니다.

  ![트랜잭션이 없는 트랜잭션 목록](images/setup06-0206.png)

트랜잭션을 발견하고 설명하는 것에 대한 정보는 [트랜잭션 설명](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view)을 참조하십시오.

## 관련 정보
{: #as-info}

- 편향성에 대한 자세한 내용은 [공정성](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)을 참조하십시오.
- 모델이 결과를 얼마나 잘 예상하는지에 대한 자세한 내용은 [정확성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)을 참조하십시오.
- 차트 및 데이터 해석에 대한 자세한 내용은 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-it-ov)을 참조하십시오.
- 기본 요인이 결과에 영향을 미치는 방법에 대한 자세한 내용은 [설명 가능성 모니터링](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)을 참조하십시오.
