---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Configure despliegues de activos utilizando archivos de configuración de JSON
{: #cf-ov}

Puede importar un archivo JSON para crear y configurar todos los despliegues del activo para fines de supervisión. También puede exportar el archivo de configuración para configurar otros activos y sus despliegues.
{: shortdesc}

Para ver un buen ejemplo de cómo trabajar con un archivo JSON, consulte el cuaderno [Python de Watson OpenScale One API Shot para suscripción](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20One%20API%20Shot%20for%20subscription.ipynb). El cuaderno describe cómo crear y configurar un despliegue de activo de Amazon SageMaker utilizando un archivo JSON en una única llamada de API. El resto de este tema hace referencia a este cuaderno.

## Cargar el contenido del archivo JSON como un diccionario Python
{: #cf-load-as-dict}

Para este ejemplo, el archivo `sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json` define los datos de configuración de un modelo que predice tipos de cáncer.

- Cargar el archivo en Python

    ```python
    configuration_file_path = 'sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json'

  con open(configuration_file_path, 'r') como fp:
      subscription_configuration = json.load(fp)
    ```

El archivo contiene datos de configuración, un ejemplo de los cuales se muestra a continuación. Consulte el cuaderno para ver un ejemplo completo del contenido de configuración.

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

## Importe desde el archivo de configuración
{: #cf-subscribe}

- Ahora, ejecute la llamada para añadir y configurar el despliegue de activo para el despliegue del modelo de predicción de cáncer de mama de ejemplo.

    ```python
    subscription = client.data_mart.subscriptions.import_configuration(binding_uid=binding_uid, configuration_data=subscription_configuration)
    ```

  El parámetro `binding_uid` es opcional si sólo hay vinculado un motor de aprendizaje automático.
  {: note}

## Exportación al archivo de configuración
{: #cf-export}

- También puede exportar el archivo de configuración como JSON:

    ```python
    exported_configuration = client.data_mart.subscriptions.export_configuration(binding_uid=binding_uid, subscription_uid=subscription.uid)
    ```

## Resultados
{: #cf-results}

El despliegue de activo se crea y configura para que lo utilice {{site.data.keyword.aios_short}}.

Consulte información más completa en la [documentación del cliente Python de {{site.data.keyword.aios_short}}![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://ai-openscale-python-client-dev.mybluemix.net/#subscriptions){: new_window}.

También puede importar y exportar configuraciones a {{site.data.keyword.aios_short}} utilizando los métodos de API de [suscripción de importación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/ai-openscale#import-subscription){: new_window} y de [suscripción de exportación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/ai-openscale#export-subscription){: new_window}.
