---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: JSON, configuration, configuring, deployment

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

# 使用 JSON 文件配置部署预订
{: #cf-ov}

您可以导入 JSON 文件，从而在创建预订期间以编程方式配置所有监视器和功能部件。您还可以导出配置文件。
{: shortdesc}

有关如何使用 JSON 文件来预订部署的良好示例，请参阅 [Watson OpenScale One API Shot for subscription Python 笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20One%20API%20Shot%20for%20subscription.ipynb)。该笔记本描述如何在单个 API 调用中使用 JSON 文件来配置 Amazon SageMaker 资产预订。本主题的其余部分会引用此笔记本。

## 将 JSON 文件内容作为 Python 字典装入
{: #cf-load-as-dict}

对于此示例，文件 `sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json` 定义用于预测癌症类型的模型的配置数据。

- 在 Python 中装入文件

    ```python
    configuration_file_path = 'sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json'

  with open(configuration_file_path, 'r') as fp:
      subscription_configuration = json.load(fp)
    ```

该文件包含配置数据，其示例如下所示。请参阅笔记本以获取配置内容的完整示例。

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

## 从配置文件添加预订
{: #cf-subscribe}

- 现在，运行调用以添加和配置样本乳腺癌预测模型部署的预订。

    ```python
    subscription = client.data_mart.subscriptions.import_configuration(binding_uid=binding_uid, configuration_data=subscription_configuration)
    ```

  如果仅绑定了一个 ML 引擎，`binding_uid` 参数即为可选。
  {: note}

## 导出 JSON 文件
{: #cf-export}

- 您还可以将配置文件导出为 JSON：

    ```python
    exported_configuration = client.data_mart.subscriptions.export_configuration(binding_uid=binding_uid, subscription_uid=subscription.uid)
    ```

## 结果
{: #cf-results}

系统将创建预订，并将已部署的模型配置为供 {{site.data.keyword.aios_short}} 使用。

请参阅 [{{site.data.keyword.aios_short}} Python 客户机文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ai-openscale-python-client-dev.mybluemix.net/#subscriptions){: new_window} 中的更多完整信息。

您还可以使用[导入预订 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/ai-openscale#import-subscription){: new_window} 和[导出预订 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/ai-openscale#export-subscription){: new_window} 方法将配置导入到 {{site.data.keyword.aios_short}} 以及从中导出配置。
