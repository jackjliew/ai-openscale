---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# 비{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 서비스 인스턴스의 페이로드 로깅
{: #cml-connect}

사용자의 AI 모델이 {{site.data.keyword.pm_full}} 이외의 기계 학습 엔진에 배치되면 Python 클라이언트로 외부 기계 학습 엔진에 대해 로깅할 수 있도록 설정해야 합니다.
{: shortdesc}

[{{site.data.keyword.aios_short}} Python 클라이언트 문서](http://ai-openscale-python-client.mybluemix.net/){: external} 및 [{{site.data.keyword.aios_short}} 튜토리얼](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}의 일부인 샘플 {{site.data.keyword.aios_short}} Python 클라이언트 노트북에서 전체 정보를 볼 수 있습니다.

## 시작하기 전에
{: #cml-prereq}

모델의 편향성을 모니터하려면 Db2 또는 {{site.data.keyword.cos_full}}에서 사용 가능한 모델의 훈련 데이터가 필요합니다. Python 함수에 대해 설명 가능성 및 정확성은 지원되지 않습니다. 훈련 데이터에 대한 자세한 정보는 [{{site.data.keyword.aios_short}}에서 내 훈련 데이터에 액세스해야 하는 이유는 무엇입니까?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)를 참조하십시오.

- {{site.data.keyword.aios_short}}을 가져와서 시작하십시오.

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  인증 정보는 "[인증 정보 작성](/docs/services/ai-openscale?topic=ai-openscale-cred-create)" 주제의 단계에 따라 찾을 수 있습니다.

- 사용자의 PostgreSQL 데이터베이스에서 스키마 이름을 작성하십시오.

- datamart를 설정하십시오.

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## 다음 단계
{: #cml-next}

- {{site.data.keyword.aios_short}} 클라이언트로 계속 진행하려면 [정확성 또는 품질 모니터 구성](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)을 참조하십시오.
- Python 명령 라이브러리를 계속 사용하려면 [Python 클라이언트 문서](http://ai-openscale-python-client.mybluemix.net/){: external}를 참조하십시오.
