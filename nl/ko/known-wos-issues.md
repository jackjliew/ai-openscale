---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}}의 알려진 문제점과 제한사항
{: #rn-12ki}

다음 목록에는 {{site.data.keyword.aios_full}}의 알려진 문제점과 제한사항이 포함되어 있습니다.
{: shortdesc}

<p>&nbsp;</p>

## 제한사항
{: #wos-limitations}

- {{site.data.keyword.aios_short}}에서는 Python SDK를 사용하여 추가 엔진을 구성하는 경우 여러 기계 학습 엔진을 지원합니다.

- 현재 릴리스는 하나의 데이터베이스, 하나의 {{site.data.keyword.pm_full}} 인스턴스 및 하나의 {{site.data.keyword.aios_short}} 인스턴스만 지원합니다.

- 데이터베이스 및 {{site.data.keyword.pm_full}} 인스턴스가 동일한 {{site.data.keyword.cloud_notm}} 계정에 배치되어야 합니다.

- Lite(무료) 플랜은 다음과 같은 월별 한계가 있습니다.

    - 두 개의 배치된 모델이 모니터링됨
    - 20개의 트랜잭션이 설명됨
    - 50,000개의 페이로드 레코드(누적)
    - 50,000개의 피드백 레코드(누적)

- {{site.data.keyword.aios_short}}은 PostgreSQL 또는 Db2 데이터베이스를 사용하여 모델 관련 데이터(피드백 데이터, 스코어링 페이로드) 및 계산된 메트릭을 저장합니다. Lite Db2 플랜은 현재 지원되지 않습니다.

- {{site.data.keyword.aios_short}}의 인스턴스당 20개의 배치된 모델이라는 라이센스 한계가 있습니다.

- {{site.data.keyword.pm_full}}의 경우, 페이로드 로깅을 위해 전송되는 이미지 분류 모델에 대한 스코어링 입력은 1MB를 초과할 수 없습니다. 제한시간 문제를 방지하려면, 이미지가 125 x 125픽셀을 초과하지 않아야 하며 첫 번째 이미지가 완료되면 두 번째 이미지에 대한 설명이 요청되도록 순차적으로 전송해야 합니다.

- 무료 Lite 플랜 데이터베이스는 GDPR을 준수하지 않습니다. 모델에서 개인 식별 가능 정보(PII)를 처리하는 경우 새 데이터베이스를 구매하거나 GDPR 규칙을 준수하는 기존 데이터베이스를 사용해야 합니다. 

- 일본어, 중국어, 한국어와 같은 연속적 스크립트 언어의 경우 공백 또는 구두점 문자로 단어를 구분하지 않으므로 비정형 텍스트 모델에 대한 설명 가능성이 지원되지 않습니다. 



<p>&nbsp;</p>

## 일반적인 문제
{: #wos-common-issues}

다음 문제는 {{site.data.keyword.Bluemix}} 및 {{site.data.keyword.wos4d_full}}의 두 {{site.data.keyword.aios_full}} 모두에 공통입니다.

<p>&nbsp;</p>

### 페이로드 형식
{: #wos-common-issues-payloadformat}

페이로드 분석의 적절한 처리를 위해 {{site.data.keyword.aios_short}}에서는 큰따옴표(")가 있는 열 이름을 페이로드에 사용하는 것을 지원하지 않습니다. 이는 CSV 및 JSON 형식의 피드백 데이터 및 스코어링 페이로드에 영향을 미칩니다. 

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- 두 가지 유형의 Azure 기계 학습 웹 서비스 중에서 `신규` 유형만 {{site.data.keyword.aios_short}}에 의해 지원됩니다. `일반` 유형은 지원되지 않습니다.

- __*기본 입력 이름이 사용되어야 함*__: Azure 웹 서비스에서 기본 입력 이름은 `"input1"`입니다. 현재 이 필드는 {{site.data.keyword.aios_short}}에 필수이며 누락되는 경우 {{site.data.keyword.aios_short}}이 작동하지 않습니다.

  Azure 웹 서비스가 기본 이름을 사용하지 않는 경우, 입력 필드 이름을 `"input1"`로 변경하면 코드가 작동합니다.

- 예를 들어 웹 서비스가 여러 개일 때 기계 학습 모델을 나열하기 위해 Microsoft Azure ML Studio를 호출하면 응답의 제한시간이 초과되는 경우, 제한시간 값을 늘려야 합니다. 예를 들어 HAProxy 로드 밸런서를 사용하는 경우 다음 명령을 실행하여 이 문제를 임시로 해결해야 합니다.

   - 로드 밸런서 노드에 로그인하고 `/etc/haproxy/haproxy.cfg`를 업데이트하여 클라이언트 및 서버 제한시간을 `1m`에서 `5m`으로 설정하려면 다음을 수행하십시오.

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - `systemctl restart haproxy`를 실행하여 HAProxy 로드 밸런서를 다시 시작하십시오.

쇼HAProxy 이외의 로드 밸런서를 사용하는 경우 비슷한 방식으로 제한시간 값을 조정해야 할 수도 있습니다.
      {: note}

- 두 가지 유형의 Azure 기계 학습 웹 서비스 중에서 `신규` 유형만 {{site.data.keyword.aios_short}}에 의해 지원됩니다. `일반` 유형은 지원되지 않습니다.

- Azure 웹 서비스에서 기본 입력 이름은 `"input1"`입니다. 현재 이 필드는 {{site.data.keyword.aios_short}}에 필수이며, 이 필드를 누락하면 정확도 모니터링에 실패합니다.

   Azure 웹 서비스에서 기본 이름을 사용하지 않으면 입력 필드 이름을 `"input1"`로 변경하십시오.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*BlazingText 알고리즘이 지원되지 않음*__: Amazon SageMaker BlazingText 알고리즘 입력 페이로드 형식이 현재 {{site.data.keyword.aios_short}} 릴리스에서 지원되지 않습니다.

<p>&nbsp;</p>


### 사용자 정의 기계 학습 서비스 인스턴스
{: #wos-common-issues-custom}

- [Python 모듈](/docs/services/ai-openscale?topic=ai-openscale-as-module)에서 현재 사용자 정의 서비스 인스턴스에 대해 설명 가능성이 작동하지 않습니다. 이는 사용자 정의 서비스 인스턴스가 모듈 스크립트에 포함되지 않은 응답 데이터 내의 숫자 예측을 요구하기 때문입니다.

<p>&nbsp;</p>


- **올바르지 않은 코드 스니펫**

    - 모니터 구성에 제공된 cURL과 Python 코드 스니펫이 둘 다 올바르지 않습니다. 정정 코드 스니펫이 다음과 같이 제공됩니다.

      *페이로드 로깅*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken", that you will use as {icp_token} in the following payload logging request 
      # TODO: manually define and pass:
      # request - input to scoring endpoint in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # response - output from scored model in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *피드백 로깅*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken" key that you will use as {icp_token} in the following payload logging request
      # TODO: manually define and pass:
      # fields - list of fields names - replace sample values with proper ones
      # values - feedback data records - replace sample values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - 편향성 제거 엔드포인트에 제공된 Java 코드 스니펫이 올바르지 않습니다. 정정 코드 스니펫이 다음과 같이 제공됩니다.

      *편향성 제거 엔드포인트*

      ```java
      /**
      At runtime you need to replace values for the following

      <HOSTNAME> - Host Name eg: aiopenscale.test.cloud.ibm.com
      <PORT> - Server Port
      <DATA_MART_ID> - DataMart id
      <SERVICE_BINDING_ID> - Service Binding id
      <ASSET_ID> - Asset id or the model id
      <DEPLOYMENT_ID> - Deployment id
      <TOKEN> - Bearer token

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


## {{site.data.keyword.wos4d_notm}}의 알려진 문제
{: #rn-16April2019ki}

다음 문제는 {{site.data.keyword.wos4d_full}}에 고유합니다.

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services(C&DS)
{: #rn-16April2019ki-icp-spss}

- **제한된 설명 가능성 지원**

   - 설명 가능성은 모든 클래스의 확률을 리턴하는 SPSS 다중 클래스 모델과 2진 모델에 지원됩니다. 
   - 설명 가능성은 우선하는 클래스 확률만 리턴하는 SPSS 다중 클래스 모델에는 지원되지 않습니다.


<p>&nbsp;</p>


- **배치 ID에는 IBM SPSS Collaboration and Deployment Services(C&DS)의 밑줄(_) 문자가 포함될 수 없음**

    - 구독할 `deployment_id`에서 밑줄(_) 문자를 제거하십시오.

<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services(C&DS)(2진 유형만 해당)에서는 추가 페이로드 요청을 수행해야 함**

    - IBM SPSS Collaboration & Deployment Services 2진 구독의 경우 [배치를 위해 모니터 준비](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config) 또는 모든 모니터를 구성한 후 또 다른 [페이로드 로깅(스코어링)을 요청](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)해야 합니다. 그러면 [설명 가능성](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov)이 정확하게 됩니다.

<p>&nbsp;</p>


- **IBM SPSS C&DS(2진 유형만 해당) 정정 레코드 수가 잘못될 수 있음**

    - IBM SPSS Collaboration & Deployment Services 2진 구독의 경우 **트랜잭션 보기** 단추를 사용하여 볼 때 *정정된 레코드* 수가 정확하지 않을 수 있습니다.

<p>&nbsp;</p>

### 지표
{: #rn-16April2019ki-icp-metrics}

- **{{site.data.keyword.pm_full}} 성능 지표가 수집되지 않음**

    - Cloud Pak for Data 환경에서 {{site.data.keyword.pm_full}}의 성능 지표는 수집되지 않습니다.

<p>&nbsp;</p>

- **설명 가능성 지원 제한사항**

    - 모델을 빌드할 때 대상(레이블) 열을 스코어링을 위한 입력 요청에 포함하지 마십시오. 모델에서 입력 요청에 대상 열을 포함시켜야 하는 경우 편향성 검사, 편향성 제거 및 설명 가능성이 작동하지 않습니다.


<p>&nbsp;</p>


### Python 함수
{: #rn-16April2019ki-icp-python}

- **지원되지 않는 Python 함수**

    - 편향성 검사, 편향성 제거 및 설명 가능성은 현재 릴리스에서 Python 함수에 지원되지 않습니다.

<p>&nbsp;</p>


### 설치 및 구성
{: #rn-16April2019ki-icp-install}


- **설치 제거 스크립트에서 Kafka 주제를 삭제하지 않음**

    - 설치 제거 스크립트를 실행해도 설치 중에 EventStream에 작성된 {{site.data.keyword.aios_short}} Kafka 주제를 제거하지 않습니다.

<p>&nbsp;</p>

### 데이터베이스
{: #rn-16April2019ki-icp-dbs}

- **Db2 Warehouse를 사용하는 행 크기 제한사항**

    - Db2 Warehouse의 경우 1MB 행 크기 제한이 있습니다. 텍스트 열(VARCHAR당 32000바이트)이 여러(30개 초과) 개인 경우 한계가 초과됩니다. SageMaker 고유 형식에서 모든 열은 문자열 형식이므로 이 제한사항은 Amazon SageMaker를 사용할 때 가장 두드러집니다.

       {{site.data.keyword.aios_short}}에서 데이터베이스 오브젝트를 작성하는 데 기본 테이블스페이스를 사용하므로 실제 한계는 데이터베이스 구성에 따라 다릅니다. 이 제한사항에 관한 추가 정보는 [IBM Knowledge Center Db2 문서](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html)에서 사용할 수 있습니다.





## 브라우저 지원
{: #abt-browser}

{{site.data.keyword.aios_short}} 서비스 도구 사용에는 {{site.data.keyword.cloud_notm}}에서 요구하는 대로 동일한 레벨의 브라우저 소프트웨어가 필요합니다. 세부사항은 {{site.data.keyword.cloud_notm}} [필수 소프트웨어](/docs/overview?topic=overview-prereqs-platform#browsers) 주제를 참조하십시오.

<p>&nbsp;</p>


## Python 클라이언트
{: #abt-python}

[{{site.data.keyword.aios_short}} Python 클라이언트](http://ai-openscale-python-client.mybluemix.net/){: external}는 {{site.data.keyword.aios_short}} 서비스를 사용하여 직접 작업할 수 있게 하는 Python 라이브러리입니다. {{site.data.keyword.aios_short}} 클라이언트 UI 대신 Python 클라이언트를 사용하여 직접 데이터 마트 데이터베이스를 구성하고 기계 학습 엔진을 바인드하고 배치를 선택 및 모니터할 수 있습니다. 이 방법으로 Python 클라이언트를 사용하는 예를 보려면 [{{site.data.keyword.aios_short}} 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)을 참조하십시오.

<p>&nbsp;</p>
## 다음 단계
{: #abt-next}

- 서비스 [시작하기](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started)
- [API 참조 자료](https://{DomainName}/apidocs/ai-openscale){: external}를 보십시오.

다른 질문이 있으십니까? 

- [새로운 기능](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [IBM에 문의](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}하십시오.
