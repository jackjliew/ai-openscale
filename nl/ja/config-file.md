---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: JSON, configuration, configuring, deployment, subscription

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

# JSON 構成ファイルを使用したアセットのデプロイメントの構成
{: #cf-ov}

JSON ファイルをインポートして、アセットのすべてのデプロイメントを作成してモニター用に構成できます。 他のアセットとそれらのデプロイメントを構成するために、構成ファイルをエクスポートすることもできます。
{: shortdesc}

JSON ファイルを処理する方法の優れた例については、[Watson OpenScale One API Shot for subscription Python notebook](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20One%20API%20Shot%20for%20subscription.ipynb) を参照してください。 このノートブックでは、JSON ファイルを使用して 1 回の API 呼び出しで Amazon SageMaker アセットのデプロイメントを作成して構成する方法を説明しています。 このトピックの以降の部分では、このノートブックを参照します。

## Python 辞書としての JSON ファイル内容のロード
{: #cf-load-as-dict}

この例では、ファイル `sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json` で、がんの種類を予測するモデルの構成データを定義します。

- Python でファイルをロードします

    ```python
    configuration_file_path = 'sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json'

  with open(configuration_file_path, 'r') as fp:
      subscription_configuration = json.load(fp)
    ```

このファイルには、以下の例に示すような構成データが含まれます。 構成コンテンツの完全な例を確認する場合は、ノートブックを参照してください。

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

## 構成ファイルからのインポート
{: #cf-subscribe}

- 次に、サンプルの乳がん予測モデル・デプロイメント用のアセットのデプロイメントを追加して構成するための呼び出しを実行します。

    ```python
    subscription = client.data_mart.subscriptions.import_configuration(binding_uid=binding_uid, configuration_data=subscription_configuration)
    ```

  `binding_uid` パラメーターは、バインドされる ML エンジンが 1 つのみの場合にはオプションです。
  {: note}

## 構成ファイルへのエクスポート
{: #cf-export}

- 構成ファイルを JSON としてエクスポートすることもできます。

    ```python
    exported_configuration = client.data_mart.subscriptions.export_configuration(binding_uid=binding_uid, subscription_uid=subscription.uid)
    ```

## 結果
{: #cf-results}

アセットのデプロイメントが作成されて、{{site.data.keyword.aios_short}} で使用するための構成が行われます。

さらに詳しい情報については、[{{site.data.keyword.aios_short}} Python クライアント資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client-dev.mybluemix.net/#subscriptions){: new_window} を参照してください。

{{site.data.keyword.aios_short}} との間の構成のインポートとエクスポートは、[サブスクリプションのインポート ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale#import-subscription){: new_window} および[サブスクリプションのエクスポート ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale#export-subscription){: new_window} の API メソッドを使用して行うこともできます。
