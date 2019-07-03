---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Infraestructuras de Amazon SageMaker
{: #frmwrks-aws-sage}

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de Amazon SageMaker:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Nativa | Clasificación | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}


## Adición de Amazon SageMaker a {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con Amazon SageMaker utilizando uno de los métodos siguientes:

- Si es la primera vez que añade un proveedor de aprendizaje automático a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Cuadernos de ejemplo
{: #frmwrks-aws-sage-smpl-ntbks}

Los cuadernos siguientes muestran cómo trabajar con Amazon SageMaker:

- [Creación y despliegue de un modelo de predicción de riesgo crediticio](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## Explorar más
{: #frmwrks-aws-sage-mediumblogs}

[Supervisar el aprendizaje automático de Sagemaker con Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
