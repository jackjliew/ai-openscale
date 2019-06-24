---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: feedback data, data, feedback, models

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

# {{site.data.keyword.aios_short}}에서 피드백 데이터 형식화 및 업로드
{: #fmt-upld-fdbk-data}

피드백 데이터는 편향성 없는 모델의 유지보수에 반드시 필요합니다. 정기적으로 {{site.data.keyword.aios_full}} 서비스에 피드백 데이터를 업로드하여 예측 애플리케이션의 컨텍스트에서 변경사항을 표시할 수 있는 최신 데이터를 모델을 고려하도록 보장해야 합니다. 피드백 루프를 사용하여 시스템은 예측의 유효성을 모니터링하고 필요하면 재훈련을 실시하여 지속적으로 학습합니다. 결과 피드백의 모니터링과 사용은 기계 학습의 핵심입니다. 피드백 데이터의 형식화 및 업로드에 도움이 되도록 다음의 정보가 제공됩니다.
(: shortdesc)

## 피드백 데이터 형식화
{: #fmt-upld-fdbk-data-fmt}

피드백 데이터를 제대로 읽으려면 이를 올바르게 형식화해야 합니다. {{site.data.keyword.aios_short}} 서비스는 다음의 형식을 허용합니다. 

- UI 또는 REST API를 사용하여 업로드가 가능한 CSV 파일 형식
- REST API를 사용해서만 업로드가 가능한 JSON 파일 형식

이러한 파일 형식은 구독 세부사항에서 사용 가능한 `training_data_schema` 스키마로 정의됩니다. 
`training_data_schema`를 보려면 Python API를 사용하여 다음 명령을 실행하십시오. 

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

훈련 데이터 스키마를 피드백 스키마와 비교하기 위해 피드백 스키마 보기를 원할 수도 있습니다. 피드백 스키마를 보려면 Python API를 사용하여 다음 명령을 실행하십시오. 

```
subscription.feedback_logging.print_table_schema()
```


### CSV 형식
{: #fmt-upld-fdbk-data-fmt-csv}

일반적으로 CSV 파일의 경우에는 다수의 열 이름에 대한 하나의 행으로 열 및 행의 데이터를 제공합니다. 

일반적으로 열 이름이 모두 대문자이면 따옴표가 필요하지 않으며, 이는 Db2의 경우 대소문자를 구분하지 않도록 합니다. 그러나 기타 데이터베이스의 경우와 열 이름이 대소문자 혼합인 인스턴스에서는 대소문자가 일치해야 합니다.
파일에 열 이름이 포함되면 열이 테이블 순서와 반드시 일치할 필요가 없지만, 파일에 열 이름이 없으면 테이블 순서와 일치해야 합니다. 원래 훈련 데이터에 없는 열을 보유할 수 있습니다. 이러한 열은 처리 중에 무시됩니다. 


### JSON 형식
{: #fmt-upld-fdbk-data-fmt-json}

JSON 형식은 열 이름에 대응되는 필드의 오브젝트 콜렉션으로 구성됩니다. 

