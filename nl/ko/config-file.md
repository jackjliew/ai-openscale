---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: JSON, configuration, configuring, deployment, subscription

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

# JSON 구성 파일을 사용하여 자산 배치 구성
{: #cf-ov}

JSON 파일을 가져와서 모니터링을 위해 모든 자산의 배치를 작성하고 구성할 수 있습니다. 또한 다른 자산 및 배치를 구성하기 위해 구성 파일을 내보낼 수도 있습니다.
{: shortdesc}

JSON 파일에 대해 작업하는 방법에 대한 좋은 예는 [Watson OpenScale One API Shot for subscription Python notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20One%20API%20Shot%20for%20subscription.ipynb)을 참조하십시오. Notebook에서는 JSON 파일을 사용하여 단일 API 호출로 Amazon SageMaker 자산 배치를 작성하고 구성하는 방법에 대해 설명합니다. 이 주제의 나머지 부분은 이 노트북을 참조합니다.

## JSON 파일 컨텐츠를 Python 사전으로 로드하십시오.
{: #cf-load-as-dict}

이 예의 경우, `sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json` 파일이 암 유형을 예측하는 모델의 구성 데이터를 정의합니다.

- 파일을 Python으로 로드하십시오.

    ```python
    configuration_file_path = 'sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json'

  with open(configuration_file_path, 'r') as fp:
      subscription_configuration = json.load(fp)
    ```

파일에는 구성 데이터가 포함되어 있습니다. 다음 예를 참조하십시오. 구성 컨텐츠의 전체 예를 보려면 노트북을 참조하십시오.

  ```python
  {'asset': {'asset_id': '0530ab0cd4f4dd5486b19c08df8b6914',
  'asset_type': 'model',
  'created_at': '2018-10-10T14:31:44.348Z',
  'name': 'DEMO-multi-classification-2018-10-10-14-26-26',
  'url': 's3://sagemaker-us-east-1-014862798213/sagemaker/DEMO-breast-cancer-prediction/DEMO-multi-classification-2018-10-10-14-26-26/output/model.tar.gz'},
 'asset_properties': {'categorical_fields': [],
  'feature_fields': ['radius_mean',
   'texture_mean',
   . . .

  'input_data_schema': {'fields': [{'metadata': {'modeling_role': 'feature'},
     'name': 'radius_mean',
     'nullable': True,
     'type': 'double'},
    {'metadata': {'modeling_role': 'feature'},
     'name': 'texture_mean',
     'nullable': True,
     'type': 'double'},
   . . .

  'input_data_type': 'structured',
  'label_column': 'diagnosis',
  'output_data_schema': {'fields': [{'metadata': {'modeling_role': 'feature'},
     'name': 'radius_mean',
     'nullable': True,
     'type': 'double'},
    {'metadata': {'modeling_role': 'feature'},
     'name': 'texture_mean',
     'nullable': True,
     'type': 'double'},
   . . .

  'prediction_field': 'predicted_label',
  'prediction_probability_field': 'score',
  'problem_type': 'multiclass',
  'training_data_schema': {'fields': [{'metadata': {'modeling_role': 'feature'},
     'name': 'radius_mean',
     'nullable': True,
     'type': 'double'},
    {'metadata': {'modeling_role': 'feature'},
     'name': 'texture_mean',
     'nullable': True,
     'type': 'double'},
   . . .

 'configurations': {'explainability': {'training_statistics': {'base_values': {'0': 13.37,
     '1': 18.84,
     '10': 0.3242,
   . . .

  'fairness_monitoring': {'class_label': 'predicted_label',
   'distributions': [{'attribute': 'radius_mean',
     'class_labels': [{'counts': [{'class_value': 'B', 'count': 1}],
       'label': '[6.8, 7.2]'},
      {'counts': [{'class_value': 'B', 'count': 3}], 'label': '[7.6, 8.0]'},
      {'counts': [{'class_value': 'B', 'count': 2}], 'label': '[8.0, 8.4]'},
   . . .

   'favourable_class': ['M'],
   'features': [{'feature': 'radius_mean',
     'majority': [[0.0, 10.0], [19.0, 20.0]],
     'minority': [[15.0, 16.0]],
     'threshold': 0.8,
     'type': 'float'}],
   'min_records': 5,
   'perform_debias': True,
   'run_status': 'INITIATED',
   'training_data_class_label': None,
   'unfavourable_class': ['B']},
  'payload_logging': {'dynamic_schema_update': True,
   'output_data_schema': {'fields': [{'metadata': {'modeling_role': 'feature'},
      'name': 'radius_mean',
      'nullable': True,
      'type': 'double'},
     {'metadata': {'modeling_role': 'feature'},
      'name': 'texture_mean',
      'nullable': True,
      'type': 'double'},
   . . .

  'performance_monitoring': {},
  'quality_monitoring': {'evaluation_definition': {'method': 'multiclass',
    'threshold': 0.8},
   'min_feedback_data_size': 5,
   'scheduleId': '63c7f400-aa29-4539-91ad-8a4b9d2b9a51'}},
 'deployments': [{'created_at': '2018-10-10T14:39:21.421Z',
   'deployment_id': '37a83f399e6dc3b9d08d7d01fe690665',
   'deployment_rn': 'arn:aws:sagemaker:us-east-1:014862798213:endpoint/demo-multi-classification-endpoint-201810101439',
   'deployment_type': 'online',
   'name': 'DEMO-multi-classification-endpoint-201810101439',
   'scoring_endpoint': {'request_headers': {'Content-Type': 'application/json'},
    'url': 'DEMO-multi-classification-endpoint-201810101439'},
   'url': 'DEMO-multi-classification-endpoint-201810101439'}],
 'export_info': {'api_version': 'v1',
  'origin': '/v1/data_marts/b73545e6-0a6e-466c-8cd0-c47c044c5702/service_bindings/bf44cc7f-990d-4942-bfc6-cbcf71a1b78c/subscriptions/0530ab0cd4f4dd5486b19c08df8b6914',
  'timestamp': '2019-02-11T11:41:01.613Z'}}
  ```

## 구성 파일에서 가져오기
{: #cf-subscribe}

- 이제 호출을 실행하여 샘플 유방암 예측 모델 배치에 대한 자산 배치를 추가하고 구성하십시오.

    ```python
    subscription = client.data_mart.subscriptions.import_configuration(binding_uid=binding_uid, configuration_data=subscription_configuration)
    ```

  ML 엔진이 하나만 바인드되는 경우, `binding_uid` 매개변수가 선택사항입니다.
  {: note}

## 구성 파일로 내보내기
{: #cf-export}

- 구성 파일을 JSON으로 내보낼 수 있습니다.

    ```python
    exported_configuration = client.data_mart.subscriptions.export_configuration(binding_uid=binding_uid, subscription_uid=subscription.uid)
    ```

## 결과
{: #cf-results}

자산 배치가 작성되고 {{site.data.keyword.aios_short}}에서 사용하도록 구성됩니다.

## 다음 단계
{: #cf-results-nxt-steps}

[{{site.data.keyword.aios_short}} Python 클라이언트 문서](http://ai-openscale-python-client-dev.mybluemix.net/#subscriptions){: external}에서 더 자세한 정보를 확인하십시오.

[구독 가져오기](https://{DomainName}/apidocs/ai-openscale#import-subscription){: external} 및 [구독 내보내기](https://{DomainName}/apidocs/ai-openscale#export-subscription){: external} API 메소드를 사용하여 {{site.data.keyword.aios_short}}에 구성을 가져오고 내보낼 수도 있습니다.
