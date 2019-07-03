---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, fast start

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

# 대화식 설정 튜토리얼
{: #gs-obj}

이 튜토리얼에서는 다음 단계를 수행합니다.

- [{{site.data.keyword.Bluemix_notm}} 기계 학습 및 스토리지 서비스 프로비저닝](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps).
- [Watson Studio 프로젝트를 설정하고 기계 학습 모델을 작성, 교육 및 배치](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [모델에 맞게 신뢰, 투명성 및 설명 가능성 구성 및 탐색](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios).

## 전제조건 {{site.data.keyword.Bluemix_notm}} 서비스 프로비저닝
{: #gs-prps}

이 튜토리얼을 완료하려면 {{site.data.keyword.aios_short}} 외에도 다음 계정과 서비스가 필요합니다.

**중요**: 최상의 성능을 내려면 {{site.data.keyword.aios_short}}와 동일한 지역에서 전제조건 서비스를 작성하는 것이 좋습니다. {{site.data.keyword.aios_short}}의 사용 가능 위치를 보려면 [서비스 가용성](/docs/resources?topic=resources-services_region)을 참조하십시오.

1.  {{site.data.keyword.ibmid}}로 [{{site.data.keyword.Bluemix_notm}} 계정](https://{DomainName}){: external}에 로그인하십시오.
1.  링크를 클릭하고 서비스 이름을 제공한 다음 **Lite**(무료) 플랜을 선택하고 **작성** 단추를 클릭하여 아직 계정과 연관되지 않은 다음 서비스마다 인스턴스를 작성하십시오.

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![기계 학습](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio 프로젝트 설정
{: #gs-setup}

1.  [Watson Studio 계정](https://dataplatform.ibm.com/){: external}에 로그인하고 새 프로젝트를 작성하여 시작하십시오. **새 프로젝트**를 선택하십시오.

    ![Watson Studio 프로젝트 작성](images/studio_create_proj.png)

1.  **표준** 타일을 선택하십시오.

    ![Watson Studio 표준 프로젝트 선택](images/studio_create_standard.png)

1.  프로젝트에 이름과 설명을 지정하고 이전 단계에서 작성한 Object Storage 서비스가 **스토리지** 메뉴에서 선택되어 있는지 확인하고 **작성**을 클릭하십시오.

### {{site.data.keyword.Bluemix_notm}} 서비스와 Watson 프로젝트와 연관
{: #gs-assoc}

1.  Watson Studio 프로젝트를 열고 **설정** 탭을 선택하십시오. **연관된 서비스** 섹션에서 **서비스 추가**를 클릭하고 **Watson**을 클릭하십시오.

    ![Watson 서비스 추가](images/add_watson_service.png)

1.  **기계 학습** 타일에서 **추가** 링크를 클릭하십시오.
2.  **기존** 탭의 **기본 서비스 인스턴스** 드롭 다운에서 이전에 작성한 서비스를 클릭하십시오.
3. **선택**을 클릭하십시오.

### `신용 위험` 모델 추가
{: #gs-addmod}

1.  {{site.data.keyword.DSX}}에서 프로젝트의 **자산** 탭을 선택하고 **Watson Machine Learning 모델** 섹션으로 스크롤한 다음 **새 Watson Machine Learning 모델** 단추를 클릭하십시오.

1.  **모델 유형 선택** 섹션에서 **샘플** 및 `신용 위험` 모델을 선택한 다음 **작성**을 클릭하십시오.

    ![새 Notebook 양식](images/credit-sample-model.png)

### `신용 위험` 모델 배치
{: #gs-depmod}

1.  `신용 위험` 모델 페이지에서 **배치** 탭을 클릭하고 **배치 추가**를 클릭하십시오.
1.  배치의 이름으로 `credit-risk-deploy`를 입력하고 **웹 서비스** 배치 유형을 선택하십시오.
1.  **저장**을 클릭하십시오.

## {{site.data.keyword.aios_short}} 구성
{: #gs-confaios}

### {{site.data.keyword.aios_short}} 프로비저닝
{: hide-dashboard}
{: #gs-provaios}

1.  [새 {{site.data.keyword.aios_short}} 서비스 인스턴스 프로비저닝](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/openscale.png)

2.  서비스의 이름을 지정하고 **Lite 플랜**을 선택한 다음 **작성**을 클릭하십시오.

### 기계 학습 모델에 {{site.data.keyword.aios_short}} 연결
{: #gs-ctmod}

이제 기계 학습 모델이 배치되었으므로 모델의 신뢰성 및 투명성을 보장하도록 {{site.data.keyword.aios_short}}을 구성할 수 있습니다.

1.  {{site.data.keyword.aios_short}} 인스턴스의 **관리** 탭을 선택하고 **애플리케이션 시작** 단추를 클릭하십시오. **{{site.data.keyword.aios_short}} 시작** 데모 페이지가 열립니다.
2. 이 튜토리얼의 경우 **사양합니다**를 클릭하고 **시작**을 클릭하십시오.

1.  **Watson Machine Learning** 타일을 클릭하십시오.

1.  이 튜토리얼의 경우 메뉴에서 {{site.data.keyword.pm_full}} 인스턴스를 선택하고 **다음**을 클릭하십시오.

    다른 {{site.data.keyword.pm_short}} 위치를 선택하는 옵션도 있습니다. 자세한 정보는 [{{site.data.keyword.pm_full}} 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)을 참조하십시오.
    {: note}

    ![{{site.data.keyword.pm_short}} 인스턴스 설정](images/gs-set-wml.png)

1.  이제 {{site.data.keyword.aios_short}}이 모니터할 배치된 모델을 선택할 수 있습니다. 작성하여 배치한 모델을 선택하고 **다음**을 클릭하십시오.

    ![배치된 모델 선택](images/gs-set-deploy0.png)

1.  이제 데이터베이스를 선택해야 합니다. 무료 데이터베이스 또는 기존/신규 데이터베이스의 두 가지 옵션이 있습니다. 이 튜토리얼의 경우 **{{site.data.keyword.aios_short}}에서 호스팅하는 무료 데이터베이스 사용** 타일을 선택하십시오.

    무료 데이터베이스에는 몇 가지 중요한 제한사항이 있습니다. 호스팅하는 데이터베이스에 대한 별도의 액세스 권한이 제공되지 않습니다. 데이터베이스 및 데이터에 대한 {{site.data.keyword.aios_short}} 액세스를 제공합니다. GDPR을 준수하지 않습니다. 이러한 각 옵션에 대한 전체 세부사항은 [데이터베이스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db) 주제를 참조하십시오. 기존 데이터베이스는 PostgreSQL 데이터베이스 또는 Db2 데이터베이스일 수 있습니다.
    {: tip}

    ![데이터베이스 선택](images/gs-set-lite-db2.png)

1.  요약 데이터를 검토하고 **저장**을 클릭하십시오. 프롬프트가 표시되면 확인하고 **계속 구성** 단추를 클릭하십시오.

    {{site.data.keyword.aios_short}} 인스턴스 ID와 동일한 데이터 마트 ID도 나열됩니다.
    {: tip}

    ![요약 검토](images/gs-setup-summary4.png)

1.  화면은 다음 화면 캡처와 유사합니다. GUI 메소드를 사용하여 데이터를 스코어링할 것이므로 **모니터 구성** 단추를 선택하여 설정을 완료하십시오.

    ![스코어링 요청 코드](images/gs-config-send-scoring.png)

### 모델에 샘플 데이터 세트 제공
{: #gs-samp}

모니터를 구성할 수 있으려면 모니터가 이용할 수 있는 페이로드 로깅을 생성하기 위해 모델에 대한 하나 이상의 스코어링 요청을 생성해야 합니다. 이 섹션에서 스코어링 요청을 생성하기 위해 JSON 파일 형식으로 샘플 데이터를 제공합니다.

1.  [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 파일을 다운로드하십시오.

1.  Watson Studio 프로젝트의 **배치** 탭에서 **credit-risk-deploy** 링크를 클릭하고 **테스트** 탭을 클릭한 후 JSON 입력 아이콘을 선택하십시오.

    ![JSON 테스트](images/json_test02.png)

1.  이제 다운로드한 `credit_payload_data.json` 파일을 열고 **테스트** 탭의 JSON 필드에 컨텐츠를 복사하십시오. **예측** 단추를 클릭하여 모델에 대한 교육 페이로드를 전송하고 스코어링하십시오.

    ![JSON 예측](images/json_test03.png)

### 모니터링 준비
{: #gs-prepmon}

1.  이제 {{site.data.keyword.aios_short}} 인스턴스에서 배치를 선택하고 **시작**을 클릭하십시오.

    ![배치 선택](images/config-select-deploy2.png)

1.  모델이 예측하는 답변이 있는 기능을 지정하십시오. (데이터베이스에서 테이블의 어떤 열에 예측 값 또는 레이블이 포함되어 있습니까?) 이 경우 모델이 신용 위험을 예측하므로 **위험** 열을 선택하고 **다음**을 클릭하십시오.

    ![모니터링 준비](images/config-prep-monitor.png)

1.  다음으로 모델 및 훈련 데이터에 대한 정보를 제공합니다. **다음**을 클릭하십시오.

    ![설명 준비](images/config-what-monitor.png)

1.  **데이터 유형** 메뉴에서 배치가 분석할 데이터 유형으로 **숫자/카테고리**를 선택하고 **다음**을 클릭하십시오.

    ![입력 유형 선택](images/config-input-monitor.png)

1.  숫자 또는 카테고리 데이터의 경우, 모니터를 구성하려면 모델에 대한 훈련 데이터에 대한 정보를 제공해야 합니다. **수동으로 모니터 구성**을 선택하여 훈련 데이터에 대한 연결 정보를 제공하십시오.

    ![구성 유형 선택](images/config-manual-monitor.png)

1.  알고리즘 유형은 정확성과 같은 모델 메트릭 모니터링에 중요합니다. 모델이 작성할 수 있는 예측이 "위험" 또는 "위험 없음"이므로 **2진 분류** [알고리즘 유형](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)을 선택하고 **다음**을 클릭하십시오.

    ![2진](images/binary.png)

1.  샘플 데이터에 대한 위치 정보는 다음 화면에서 미리 채워져 있습니다. **다음**을 선택하여 계속하십시오.

    ![훈련 데이터 페이지의 Db2 위치 지정](images/gs-config-train-db2-monitor.png)

1.  스키마와 테이블 또한 미리 채워져 있습니다. **다음**을 클릭하여 진행하십시오.

    ![스키마 및 교육 테이블의 Db2 위치 지정](images/gs-fair-config-table-db2.png)

1.  이제 모델이 예측할 응답을 포함하는 특성(즉, 데이터베이스에서 예측 값(레이블)을 포함하는 테이블의 컬럼)를 지정해야 합니다. 이 경우, 모델이 신용 위험을 예측하므로 **위험** 열을 선택하고 **다음**을 클릭하십시오.

    훈련 데이터베이스에는 모델을 교육하기 위해 제공한 값이 있습니다.
    {: note}

    ![예측 레이블 입력](images/gs-config-label.png)

1.  모델을 교육시키는 데 사용되는 열을 선택하십시오. 이는 모델 배치가 요청에서 예상하는 데이터입니다. `_training`을 제외하는 모든 데이터 열이 모델에 대한 입력입니다. 모든 기타 입력을 선택하고 **다음**을 클릭하십시오.

    ![설명 가능성 입력](images/explain_inputs1.png)

1.  카테고리 데이터의 경우, 원래 포함된 텍스트 값이 아니라 정수를 포함하는 열을 식별해야 합니다. 아래에 표시된 대로 값을 선택하십시오.

    ![설명 가능성 입력](images/config_categories.png)

1.  선택 요약을 검토하고 **저장**을 클릭한 다음 **확인**을 클릭하십시오.

### 공정성 모니터링 구성
{: #gs-cfgfair}

1.  **공정성**을 클릭하십시오.

1.  공정성에 대해 읽고 **다음**을 클릭하십시오. 자세한 정보는 [공정성](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)을 참조하십시오.

1.  이제 공정성을 모니터할 특성을 선택하십시오. 선택한 각 특성에 대해 {{site.data.keyword.aios_short}}이 배치된 모델의, 다른 그룹보다 한 그룹의 선호 결과를 우선하는 경향을 모니터합니다. 이 예에서는 **성별** 및 **연령** 특성을 모니터할 것입니다.

    기능은 개별적으로 모니터되지만, 임의의 편향 제거는 모든 기능의 문제를 함께 정정합니다. **성별** 및 **연령** 타일을 클릭하고 **다음**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}}은 참조 그룹과 비교하여 모니터되는 그룹에 대한 편향성을 발견합니다. **성별** 특성의 경우, **참조 그룹**에 `male` 값을 추가하고 **모니터되는 그룹**에 `female` 값을 추가한 후에 **다음**을 클릭하십시오.

    모니터되는 그룹에 대한 위험 예측 비율이 참조 그룹에 대한 비율과 다르면 모델이 **성별**에 대한 편향성이 있는 것으로 플래그를 지정합니다. 따라서 모델이 당시의 남자 고객 60% 및 여자 고객 20% 대상으로 위험을 예측하면 편향배치됩니다.

    ![성별 그룹](images/gender_groups1.png)

1.  **성별**의 공정성 임계값을 지정하십시오. 조작 대시보드에서는 공정성 등급이 사용자가 설정한 임계값을 초과하는 경우 경보를 표시합니다. 90% 임계값을 설정하고 **다음**을 클릭하십시오.

1.  **연령** 특성의 경우, **참조 그룹**에 `26-74` 값을 추가하고 **모니터되는 그룹**에 `19-25` 값을 추가한 후에 **다음**을 클릭하십시오.

    **성별**에서와 같이, 모니터되는 그룹에 대한 위험 예측 비율이 참조 그룹에 대한 비율과 다르면 모델이 **연령**에 대한 편향성이 있는 것으로 플래그를 지정합니다. 따라서 26살에서 74살 사이의 고객이 19살에서 25살 사이의 고객과 다른 비율로 위험 예측을 수신하면 모델이 편향배치됩니다.

    ![BP 그룹](images/age_groups.png)

1.  **연령**에 대해 90% 임계값을 설정하고 **다음**을 클릭하십시오.

1.  **훈련 데이터의 값** 필드에서 **선호 값** 및 **비선호 값** 필드로 값을 끌어다 놓으십시오. 이 튜토리얼의 경우, 선호 값이 **위험 없음**이며 비선호 값이 **위험**입니다. **다음**을 클릭하십시오.

    {{site.data.keyword.aios_short}}이 자동으로 페이로드 로깅 데이터베이스의 어느 열이 예측 값을 포함하는지 발견하고 **훈련 데이터의 값** 필드에 이를 제시합니다. 훈련 데이터베이스에 모델을 교육하기 위해 제공한 값이 있는 반면 페이로드 로깅 데이터베이스에는 모델 런타임 시에 수집하여 모델을 다시 교육하거나 다시 배치하기 위해 선택적으로 사용할 수 있는 피드백 데이터가 있습니다.
    {: note}

    ![양수 및 음수 값](images/pos_and_neg2.png)

1.  슬라이더를 사용하여 최소 샘플 크기를 100으로 조정하고 **다음**을 클릭하십시오.

    ![최소 크기](images/gs-fair-config-sample.png)

    이 튜토리얼의 경우 최소 샘플 크기는 100으로 설정됩니다. 일반적으로 샘플 크기가 너무 작아서 결과를 왜곡하지 않도록 더 큰 샘플 크기를 권장합니다.
    {: note}

1.  사용자의 선택을 검토하고 **저장**을 클릭한 다음 **확인**을 클릭하십시오.

    ![구성 요약](images/fair-summary.png)

    편향성을 제거한 스코어링 엔드포인트를 제공하는 창이 표시됩니다. 이 튜토리얼에서 CLI가 아니라 GUI 메소드를 사용하여 데이터를 스코어링하므로 계속하려면 **확인**을 클릭하십시오.

    ![편향성 제거 API](images/gs-insight-debias-api.png)

### 정확성 모니터링 구성
{: #gs-cfgac}

1.  **정확성**을 클릭하십시오.

1.  정확성에 대해 읽고 **다음**을 클릭하십시오. 자세한 정보는 [정확성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)을 참조하십시오.

1.  정확성 경보 임계값을 90% 로 설정하고 **다음**을 클릭하십시오.

1.  다음 화면에서 슬라이더를 사용하여 최소 샘플 크기를 10으로 조정하고 **다음**을 클릭하십시오.

    이 튜토리얼의 경우 최소 샘플 크기는 10으로 설정되어 있습니다. 일반적으로 샘플 크기가 너무 작아서 결과를 왜곡하지 않도록 더 큰 샘플 크기를 권장합니다.
    {: note}

1.  최대 샘플 크기로는 10000을 사용하십시오. **다음**을 클릭하십시오.

1.  사용자의 선택을 검토하고 **저장**을 클릭한 다음 **확인**을 클릭하십시오.

1.  마지막으로 피드백 데이터를 추가할 수 있는 옵션이 제공됩니다. 이에 대해서는 다음 절에서 설명합니다. 이제 **피드백 데이터 추가** 단추를 클리하지 않고 **확인**을 클릭하여 창을 닫으십시오.

    자세한 정보는 [정확성 모니터 구성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config)을 참조하십시오.

## 모델에 샘플 피드백 데이터 세트 제공
{: #gs-smpfeed}

정확성에 대한 모니터링을 사용으로 설정하려면 모델에 피드백 데이터를 제공해야 합니다. 그전에는 대시보드에 정확성 데이터가 표시되지 않습니다. 샘플 피드백 데이터를 스코어링 모델에 추가하여 한 번에 요청을 모두 생성할 수 있습니다. 이 작업의 경우 샘플 피드백 데이터를 포함하는 CSV 파일을 다운로드할 것입니다.

1.  [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv) 파일을 다운로드하십시오.

1.  {{site.data.keyword.aios_short}}에서 **인사이트** 탭을 클릭하십시오.

    ![인사이트](images/insight-dash-tab.png)

1.  배치된 모델에 대한 타일을 클릭하십시오.

    ![인사이트 탭 - 데이터 없음](images/gs-insight-overview.png)

1.  그런 다음 편집 아이콘을 클릭하여 배치 구성을 편집하십시오.

    ![편집 아이콘 표시](images/gs-insight-edit-icon.png)

1.  요약 사이드 패널에서 **피드백 데이터 추가** 단추를 클릭하고 다운로드한 `credit_feedback_data.csv` 파일을 선택하십시오. 구분 기호로 **쉼표(,)**를 선택하고 **확인**을 클릭하십시오.

    파일 크기가 현재 8MB로 제한됩니다.
    {: note}

    ![정확성 구분 기호](images/accuracy-delimit.png)

    CSV 파일을 추가하면 모델에 피드백 데이터가 제공됩니다.

    ![요약 패널](images/gs-insight-summary-panel-2.png)

## 결과 보기
{: #gs-viewres}

정확성 모니터링을 구성한 후 한 시간 후에 정확성 확인이 실행됩니다. 프로덕션 시스템에서 대시보드가 피드백 데이터를 누적하는 데 시간이 필요합니다. 이 튜토리얼의 경우, **인사이트** 대시보드에서 결과를 볼 수 있도록 피드백 데이터를 추가한 후에 수동으로 정확성 확인을 트리거하고자 할 것입니다.

결과를 즉시 확인하려면 **인사이트** 페이지에서 배치를 선택한 다음 **공정성 지금 확인** 또는 **품질 지금 확인** 단추를 클릭하십시오.

### 배치에 대한 인사이트 보기
{: #gs-viewin}

1. [{{site.data.keyword.aios_short}} 대시보드](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}에서 **인사이트** 탭을 클릭하십시오.

  ![인사이트](images/insight-dash-tab.png)

1. 인사이트 페이지에서 배치된 모델에 대한 메트릭 개요를 볼 수 있습니다. 공정성 또는 정확도 지표가 90% 임계값을 초과하는 경우 경보를 표시됩니다.

  공정성 및 정확성 메트릭 표시에 최대 한 시간까지 소요될 수 있습니다.
  {: tip}

  ![인사이트 개요](images/insight-overview.png)

### 배치에 대한 모니터링 데이터 보기
{: #gs-viewmon}

1.  인사이트 페이지에서 타일을 클릭하여 배치를 선택하십시오. 배치에 대한 모니터링 데이터가 표시됩니다. 참고: 피드백 .csv 파일을 업로드한 후에 공정성 또는 정확성 데이터가 업데이트되지 않았음을 발견할 수도 있습니다. 결과를 즉시 확인하려면 **공정성 지금 확인** 또는 **품질 지금 확인** 단추를 클릭하십시오.
1.  마커를 차트를 가로질러 밀어서 샘플 데이터 및 샘플 피드백 데이터를 실행한 동안의 시간 프레임에 대한 데이터를 선택하십시오. 그런 다음 **세부사항 보기**를 클릭하십시오.

    ![모니터 데이터](images/insight-monitor-data.png)

1.  다음으로, 모니터한 데이터에 대한 차트를 검토하십시오. 이 예에서는 **특성** 메뉴를 사용하여 `Age` 또는 `Sex`를 선택하여 모니터되는 데이터에 대한 세부사항을 확인하십시오.

    이러한 차트를 읽는 방법에 대한 자세한 정보는 [특정 시간 동안의 데이터 시각화](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)를 참조하십시오.
    {: tip}

    ![인사이트 개요](images/insight-review-charts.png)

### 모델 트랜잭션에 대한 설명 가능성 보기
{: #gs-viewextx}

1.  모니터한 데이터에 대한 차트에서 **트랜잭션 보기** 단추를 클릭하십시오.

    ![트랜잭션 보기](images/view_transactions.png)

1.  지난 시간 동안 편향성에 기여한 트랜잭션 목록이 표시됩니다. 특정 트랜잭션에 대한 상세한 설명을 보려면 **ACTION** 열에서 **설명**을 클릭하십시오.

    ![트랜잭션 목록](images/transaction_list_cr.png)
    
1.  모델이 결론에 도달한 방법에 대한 설명이 표시됩니다. 이 설명에는 모델의 신뢰도, 신뢰수준에 기여한 요인 및 모델에 공급된 열이 포함됩니다.

    ![트랜잭션 보기](images/view_transaction1.png)

## 관련 정보
{: #wos-info}

- 편향성에 대한 자세한 내용은 [공정성](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)을 참조하십시오.
- 모델이 결과를 얼마나 잘 예상하는지에 대한 자세한 내용은 [정확성](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)을 참조하십시오.
- 차트, 데이터 및 트랜잭션 해석에 대해 알아보려면 [공정성, 분당 평균 요청 및 정확성 모니터링](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)을 참조하십시오.
