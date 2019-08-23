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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} for {{site.data.keyword.cloud_notm}}의 알려진 문제와 제한사항
{: #rn-12ki}

다음 목록에는 {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} 및 {{site.data.keyword.wos4d_full}}에 공통되는 알려진 문제와 제한사항이 포함되어 있으며, {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}}에 특정한 알려진 문제와 제한사항도 포함되어 있습니다.
{: shortdesc}

<p>&nbsp;</p>

## 일반적인 문제
{: #wos-common-issues}

다음의 제한사항과 알려진 문제는 {{site.data.keyword.aios_full}} on {{site.data.keyword.Bluemix}} 및 {{site.data.keyword.wos4d_full}} 모두에 공통입니다. 

<p>&nbsp;</p>


### 공통 제한사항
{: #wos-limitations}

- {{site.data.keyword.pm_full}}의 경우 페이로드 로깅을 위해 전송된 이미지 분류 모델의 스코어링 입력은 ai-open-scale-ibm-aios-scheduling  | 1 | 스케줄링 서비스 MB를 초과할 수 없습니다. 제한시간 문제를 방지하려면, 이미지가 125 x 125픽셀을 초과하지 않아야 하며 첫 번째 이미지가 완료되면 두 번째 이미지에 대한 설명이 요청되도록 순차적으로 전송해야 합니다.


- 일본어, 중국어, 한국어와 같은 연속적 스크립트 언어의 경우 공백 또는 구두점 문자로 단어를 구분하지 않으므로 비정형 텍스트 모델에 대한 설명 가능성이 지원되지 않습니다.



<p>&nbsp;</p>


### 드리프트 구성 오류가 드리프트 모니터 구성을 방해함
{: #wos-common-issues-mismatchdatatype}

모델 구성 화면의 유연성으로 인해 나중에 모니터(예: 드리프트 발견 모니터) 구성을 원할 때 문제점이 발생할 수도 있습니다. 데이터 유형을 선택할 수 있으므로 모델의 원본을 반영하는 항목을 선택해야 합니다. 예측 열 유형을 제대로 선택하지 않으면 다음과 같은 오류가 발생할 수 있습니다.

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

다음과 같은 경우가 가장 가능성이 높은 원인입니다.

- `class` 레이블이 문자열 유형이고 `modeling_role` **예측**이 **예측** 열에 double 유형으로 지정됩니다. 왜냐하면 이것이 출력 데이터 스키마를 정의하는 방식이기 때문입니다.
- UI에서 double 유형의 **예측** 열을 선택했으며 이것이 제한되지 않습니다.


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


### 브라우저 지원
{: #abt-browser}

{{site.data.keyword.aios_short}} 서비스 도구 사용에는 {{site.data.keyword.cloud_notm}}에서 요구하는 대로 동일한 레벨의 브라우저 소프트웨어가 필요합니다. 세부사항은 {{site.data.keyword.cloud_notm}} [필수 소프트웨어](/docs/overview?topic=overview-prereqs-platform#browsers) 주제를 참조하십시오.

<p>&nbsp;</p>


### Python 클라이언트
{: #abt-python}

[{{site.data.keyword.aios_short}} Python 클라이언트](http://ai-openscale-python-client.mybluemix.net/){: external}는 {{site.data.keyword.aios_short}} 서비스를 사용하여 직접 작업할 수 있게 하는 Python 라이브러리입니다. {{site.data.keyword.aios_short}} 클라이언트 UI 대신 Python 클라이언트를 사용하여 직접 데이터 마트 데이터베이스를 구성하고 기계 학습 엔진을 바인드하고 배치를 선택 및 모니터할 수 있습니다. 이 방법으로 Python 클라이언트를 사용하는 예를 보려면 [{{site.data.keyword.aios_short}} 샘플 노트북](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)을 참조하십시오.


## {{site.data.keyword.aios_short}} 관련 문제
{: #cloud-issues}

다음의 제한사항과 문제는 {{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}}에 특정합니다. 

<p>&nbsp;</p>

### 제한사항
{: #cloud-limitations}

- 현재 릴리스는 하나의 데이터베이스, 하나의 {{site.data.keyword.pm_full}} 인스턴스 및 하나의 {{site.data.keyword.aios_short}} 인스턴스만 지원합니다.  

- 데이터베이스 및 {{site.data.keyword.pm_full}} 인스턴스가 동일한 {{site.data.keyword.cloud_notm}} 계정에 배치되어야 합니다.

- {{site.data.keyword.aios_short}}은 PostgreSQL 또는 Db2 데이터베이스를 사용하여 모델 관련 데이터(피드백 데이터, 스코어링 페이로드) 및 계산된 메트릭을 저장합니다. Lite Db2 플랜은 현재 지원되지 않습니다.

- 무료 Lite 플랜 데이터베이스는 GDPR을 준수하지 않습니다. 모델에서 개인 식별 가능 정보(PII)를 처리하는 경우 새 데이터베이스를 구매하거나 GDPR 규칙을 준수하는 기존 데이터베이스를 사용해야 합니다.



<p>&nbsp;</p>
## 다음 단계
{: #abt-next}

- [시작하기](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- [API 참조 자료](https://{DomainName}/apidocs/ai-openscale){: external}를 보십시오.
- [{{site.data.keyword.aios_short}}의 새로운 기능](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM에 문의](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}하십시오.
