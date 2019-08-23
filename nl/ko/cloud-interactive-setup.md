---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

이 튜토리얼에서는 필수 {{site.data.keyword.Bluemix_notm}} 서비스의 프로비저닝, Watson Studio에서 프로젝트 설정 및 샘플 모델 배치, 그리고 {{site.data.keyword.aios_short}}에서 모니터 구성을 수행하는 방법을 알아봅니다.
{: shortdesc}

1. [{{site.data.keyword.Bluemix_notm}} 기계 학습 및 스토리지 서비스 프로비저닝](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps).
2. [Watson Studio 프로젝트를 설정하고 기계 학습 모델을 작성, 교육 및 배치](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [모델에 맞게 신뢰, 투명성 및 설명 가능성 구성 및 탐색](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios).

## 전제조건 {{site.data.keyword.Bluemix_notm}} 서비스 프로비저닝
{: #gs-prps}

이 튜토리얼을 완료하려면 {{site.data.keyword.aios_short}} 외에도 다음 계정과 서비스가 필요합니다.

**중요**: 최상의 성능을 내려면 {{site.data.keyword.aios_short}}와 동일한 지역에서 전제조건 서비스를 작성하는 것이 좋습니다. {{site.data.keyword.aios_short}}의 사용 가능 위치를 보려면 [서비스 가용성](/docs/resources?topic=resources-services_region){: external}을 참조하십시오.

1.  {{site.data.keyword.ibmid}}로 [{{site.data.keyword.Bluemix_notm}} 계정](https://{DomainName}){: external}에 로그인하십시오.
1.  링크를 클릭하고 서비스 이름을 제공한 다음 **Lite**(무료) 플랜을 선택하고 **작성** 단추를 클릭하여 아직 계정과 연관되지 않은 다음 서비스마다 인스턴스를 작성하십시오.

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![기계 학습](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio 프로젝트 설정
{: #gs-setup}

1.  [Watson Studio 계정](https://dataplatform.ibm.com/){: external}에 로그인하고 새 프로젝트를 작성하여 시작하십시오. **프로젝트 작성**을 클릭하십시오.

    ![Watson Studio 프로젝트 작성](images/studio_create_proj.png)

1.  **빈 프로젝트 작성** 타일을 클릭하십시오. 
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

    ![신용 위험 타일이 표시됨](images/credit-sample-model.png)

### `신용 위험` 모델 배치
{: #gs-depmod}

1.  `신용 위험` 모델 페이지에서 **배치** 탭을 클릭하고 **배치 추가**를 클릭하십시오.
1.  배치의 이름으로 `credit-risk-deploy`를 입력하고 **웹 서비스** 배치 유형을 선택하십시오.
1.  **저장**을 클릭하십시오.

## {{site.data.keyword.aios_short}} 구성
{: #gs-confaios}

이제 기계 학습 모델이 배치되었으므로 모델의 신뢰성 및 투명성을 보장하도록 {{site.data.keyword.aios_short}}을 구성할 수 있습니다.

### {{site.data.keyword.aios_short}} 프로비저닝
{: #gs-provaios}

1.  [새 {{site.data.keyword.aios_short}} 서비스 인스턴스 프로비저닝](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  서비스의 이름을 지정하고 **Lite 플랜**을 선택한 다음 **작성**을 클릭하십시오.

1.  {{site.data.keyword.aios_short}} 인스턴스의 **관리** 탭을 선택하고 **애플리케이션 시작** 단추를 클릭하십시오. **{{site.data.keyword.aios_short}} 시작** 데모 페이지가 열립니다.
2. 이 튜토리얼의 경우 **사양합니다**를 클릭하십시오.

### 데이터베이스 선택
{: #gs-db-choice}

이제 데이터베이스를 선택해야 합니다. 무료 데이터베이스 또는 기존/신규 데이터베이스의 두 가지 옵션이 있습니다.

2. 이 튜토리얼의 경우 **무료 Lite 플랜 데이터베이스 사용** 타일을 선택하십시오.

   무료 데이터베이스에는 몇 가지 중요한 제한사항이 있습니다. 호스팅하는 데이터베이스에 대한 별도의 액세스 권한이 제공되지 않습니다. 데이터베이스 및 데이터에 대한 {{site.data.keyword.aios_short}} 액세스를 제공합니다. GDPR을 준수하지 않습니다. 이러한 각 옵션에 대한 전체 세부사항은 [데이터베이스 지정](/docs/services/ai-openscale?topic=ai-openscale-connect-db) 주제를 참조하십시오. 기존 데이터베이스는 PostgreSQL 데이터베이스 또는 Db2 데이터베이스일 수 있습니다.
    {: tip}

   ![데이터베이스 선택](images/gs-set-lite-db2.png)

1.  요약 데이터를 검토하고 **저장**을 클릭하십시오. 프롬프트가 표시되면 확인하고 **계속 구성** 단추를 클릭하십시오.

    {{site.data.keyword.aios_short}} 인스턴스 ID와 동일한 데이터 마트 ID도 나열됩니다.
    {: tip}

    ![요약 검토](images/gs-setup-summary4.png)

1.  화면은 다음 화면 캡처와 유사합니다. GUI 메소드를 사용하여 데이터를 스코어링할 것이므로 **모니터 구성** 단추를 선택하여 설정을 완료하십시오.

    ![스코어링 요청 코드](images/gs-config-send-scoring.png)

### 기계 학습 모델에 {{site.data.keyword.aios_short}} 연결
{: #gs-ctmod}


1.  **Watson Machine Learning** 타일을 클릭한 후 **저장**을 클릭하십시오.

1.  이 튜토리얼의 경우 메뉴에서 {{site.data.keyword.pm_full}} 인스턴스를 선택하고 **다음**을 클릭하십시오.

    다른 {{site.data.keyword.pm_short}} 위치를 선택하는 옵션도 있습니다. 자세한 정보는 [{{site.data.keyword.pm_full}} 서비스 인스턴스 지정](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)을 참조하십시오.
    {: note}

    ![{{site.data.keyword.pm_short}} 인스턴스 설정](images/gs-set-wml.png)

이제 {{site.data.keyword.aios_short}}이 모니터할 배치된 모델을 선택할 수 있습니다.


### 모델에 샘플 데이터 세트 제공
{: #gs-samp}

모니터를 구성할 수 있으려면 모니터가 이용할 수 있는 페이로드 로깅을 생성하기 위해 모델에 대한 하나 이상의 스코어링 요청을 생성해야 합니다. 이 섹션에서 사용자는 JSON 파일 형식으로 Watson Studio에 샘플 데이터를 제공하여 스코어링 요청을 생성합니다. 

1.  [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 파일을 다운로드하십시오.

1.  Watson Studio 프로젝트의 **배치** 탭에서 **credit-risk-deploy** 링크를 클릭하고 **테스트** 탭을 클릭한 후 JSON 입력 아이콘을 선택하십시오.

    ![JSON 테스트](images/json_test02.png)

1.  이제 다운로드한 `credit_payload_data.json` 파일을 열고 **테스트** 탭의 JSON 필드에 컨텐츠를 복사하십시오. **예측** 단추를 클릭하여 모델에 대한 교육 페이로드를 전송하고 스코어링하십시오.

    ![JSON 예측](images/json_test03.png)

## 다음 단계
{: #gs-next-steps-config}

다음 단계를 완료하여 이 튜토리얼을 계속하십시오. 

1. [배치할 모니터를 준비하십시오](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   모니터를 준비하려면 배치된 모델 중 하나를 선택하고 이를 대시보드에 추가해야 합니다. **인사이트** 탭에서 배치 타일을 클릭하거나 **대시보드에 추가** 단추를 클릭하여 배치된 모델을 선택한 후 **구성**을 클릭하십시오. 

2. [페이로드 로깅을 설정합니다](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   **페이로드 로깅** 섹션에서 입력의 유형을 지정해야 합니다. 

3. [모델 세부사항을 설정하십시오](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   **모델 세부사항** 섹션에서 모델 세부사항을 기록해야 합니다. 이 튜토리얼의 경우 **수동으로 모니터 구성**을 선택하십시오. 

4. [품질 모니터링을 구성하십시오](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   **품질** 섹션에서 품질 경보 임계값 및 샘플 크기를 설정합니다. 

5. [공정성 모니터링을 구성하십시오](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   **공정성** 섹션에서 공정성에 대해 모니터할 특성을 선택하십시오. 선택한 각 특성에 대해 {{site.data.keyword.aios_short}}이 배치된 모델의, 다른 그룹보다 한 그룹의 선호 결과를 우선하는 경향을 모니터합니다. 비록 특성이 개별적으로 모니터링되지만, 편향성 제거는 모든 특성의 문제를 함께 해결합니다. 

6. [드리프트 감지 모니터를 구성하십시오](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   **드리프트** 섹션에서 드리프트 감지 모델을 설정합니다. 
   
5. [샘플 피드백 데이터 세트를 모델에 제공하십시오](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   품질에 대한 모니터링을 사용으로 설정하려면 모델에 피드백 데이터를 제공해야 합니다. 이를 완료하기 전에는 품질 데이터가 대시보드에 표시되지 않습니다. 샘플 피드백 데이터를 스코어링 모델에 추가하여 한 번에 요청을 모두 생성할 수 있습니다. 이 작업의 경우 샘플 피드백 데이터를 포함하는 CSV 파일을 다운로드할 것입니다.

6. [인사이트를 확보하십시오](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   정확성 모니터링을 구성한 후 한 시간 후에 정확성 확인이 실행됩니다. 프로덕션 시스템에서 대시보드가 피드백 데이터를 누적하는 데 시간이 필요합니다. 이 튜토리얼의 경우, **인사이트** 대시보드에서 결과를 볼 수 있도록 피드백 데이터를 추가한 후에 수동으로 정확성 확인을 트리거하고자 할 것입니다.

   결과를 즉시 확인하려면 **인사이트** 페이지에서 배치를 선택하고 **품질** 메트릭 중 하나를 클릭한 후 **지금 품질 확인**을 클릭하십시오. 
