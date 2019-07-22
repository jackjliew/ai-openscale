---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# Definición del esquema de entrada y salida utilizando el cliente Python o la API REST
{: #schema-def}


{: shortdesc}

El esquema de datos de salida: (del cliente Python)

```
{'fields': [{'metadata': {}, 'name': 'ID', 'nullable': True, 'type': 'integer'}, {'metadata': {}, 'name': 'Gender', 'nullable': True, 'type': 'string'}, {'metadata': {}, 'name': 'Status', 'nullable': True, 'type': 'string'}, {'metadata': {}, 'name': 'Children', 'nullable': True, 'type': 'integer'}, {'metadata': {}, 'name': 'Age', 'nullable': True, 'type': 'decimal(14,6)'}, {'metadata': {}, 'name': 'Customer_Status', 'nullable': True, 'type': 'string'}, {'metadata': {}, 'name': 'Car_Owner', 'nullable': True, 'type': 'string'}, {'metadata': {}, 'name': 'Customer_Service', 'nullable': True, 'type': 'string'}, {'metadata': {}, 'name': 'Satisfaction', 'nullable': True, 'type': 'integer'}, {'metadata': {}, 'name': 'Business_Area', 'nullable': True, 'type': 'string'}, {'metadata': {'modeling_role': 'prediction'}, 'name': 'prediction', 'nullable': True, 'type': 'double'}, {'metadata': {'values': ['NA', 'Free Upgrade', 'On-demand pickup location', 'Voucher', 'Premium features'], 'modeling_role': 'decoded-target'}, 'name': 'predictedLabel', 'nullable': True, 'type': 'string'}, {'metadata': {'modeling_role': 'probability'}, 'name': 'probability', 'nullable': True, 'type': {'containsNull': True, 'elementType': 'double', 'type': 'array'}}], 'type': 'struct'}
```



## Pasos siguientes
{: #schema-def-nextsteps}

Consulte la [documentación de la API REST](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}.