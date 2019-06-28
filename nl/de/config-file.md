---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Assetbereitstellungen mit JSON-Konfigurationsdateien konfigurieren
{: #cf-ov}

Sie können eine JSON-Datei importieren, um alle Bereitstellungen Ihres Assets zu Überwachungszwecken zu erstellen und zu konfigurieren. Sie können die Konfigurationsdatei auch exportieren, um weitere Assets und deren Bereitstellungen zu konfigurieren.
{: shortdesc}

Ein gutes Anschauungsbeispiel dafür, wie Sie eine JSON-Datei verwenden, enthält das [Python-Notizbuch 'Watson OpenScale: Ein API-Aufruf für Abonnements'](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20One%20API%20Shot%20for%20subscription.ipynb). In diesem Notizbuch wird beschrieben, wie Sie eine Amazon SageMaker-Assetbereitstellung mit einer JSON-Datei in einem einzigen API-Aufruf erstellen und konfigurieren. Der Rest dieses Abschnitts bezieht sich auf dieses Notizbuch.

## Inhalt der JSON-Datei als Python-Wörterverzeichnis laden
{: #cf-load-as-dict}

Für das vorliegende Beispiel definiert die Datei `sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json` Konfigurationsdaten für ein Modell, das den Typ von Krebs vorhersagt.

- Datei in Python laden

    ```python
    configuration_file_path = 'sagemaker_native_multiclass_breast-cancer_all_monitors_sub_configuration.json'

  with open(configuration_file_path, 'r') as fp:
      subscription_configuration = json.load(fp)
    ```

Die Datei enthält Konfigurationsdaten. Ein Beispiel dieser Daten ist unten dargestellt. Ein vollständiges Beispiel für den Konfigurationsinhalt enthält das Notizbuch.

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

## Aus der Konfigurationsdatei importieren
{: #cf-subscribe}

- Führen Sie nun den Aufruf aus, um die Assetbereitstellung des Vorhersagebeispielmodells für Brustkrebs hinzuzufügen und zu konfigurieren.

    ```python
    subscription = client.data_mart.subscriptions.import_configuration(binding_uid=binding_uid, configuration_data=subscription_configuration)
    ```

  Der Parameter `binding_uid` ist optional, wenn nur eine ML-Engine gebunden wird.
  {: note}

## In die Konfigurationsdatei exportieren
{: #cf-export}

- Sie können die Konfigurationsdatei auch als JSON-Datei exportieren:

    ```python
    exported_configuration = client.data_mart.subscriptions.export_configuration(binding_uid=binding_uid, subscription_uid=subscription.uid)
    ```

## Ergebnisse
{: #cf-results}

Die Assetbereitstellung wird für die Nutzung durch {{site.data.keyword.aios_short}} erstellt und konfiguriert.

Umfassendere Informationen finden Sie in der [Dokumentation für {{site.data.keyword.aios_short}} Python-Clients ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ai-openscale-python-client-dev.mybluemix.net/#subscriptions){: new_window}.

Mithilfe der API-Methoden [Abonnement importieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/ai-openscale#import-subscription){: new_window} und [Abonnement exportieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/ai-openscale#export-subscription){: new_window} können Sie Konfigurationen auch in {{site.data.keyword.aios_short}} importieren und exportieren.
