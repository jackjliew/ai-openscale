---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Infraestructuras de Microsoft Azure ML Service
{: #frmwrks-azure-service}

{{site.data.keyword.aios_full}} da soporte completo a las siguientes infraestructuras de Microsoft Azure Machine Learning Service:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Nativa | Clasificación | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

## Adición de Microsoft Azure ML Service a {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con Microsoft Azure ML Service utilizando uno de los métodos siguientes:

- Si es la primera vez que añade un proveedor de aprendizaje automático a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


Incorporar carga útil de usuario necesaria para los metadatos.
Crear el modelo
Interfaz de usuario de incorporación para configurar la supervisión para
cargar la información de las necesidades de openscale de datos de entrenamiento/cuadernos
ejecutar el registro de carga útil,
interfaz de usuario - renovar

Responsabilidad del implementador 

MJS: Seguimiento con Lukasz y Clifford Chu

A

## Cuadernos de ejemplo
{: #frmwrks-azure-smpl-ntbks}

Los siguientes cuadernos muestran cómo trabajar con Microsoft Azure ML Service:

- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Ejemplos de puntuación de modelos de MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorar más
{: #frmwrks-azure-mediumblogs}

[Supervisar el aprendizaje automático de Azure con Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
