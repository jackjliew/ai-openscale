---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Infraestructuras de aprendizaje automático personalizadas
{: #frmwrks-custom}

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de aprendizaje automático personalizadas:
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Equivalente a {{site.data.keyword.pm_full}} | Clasificación | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

## Adición de un motor de aprendizaje automático personalizado a {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

Puede configurar {{site.data.keyword.aios_short}} para que funcione con un proveedor de aprendizaje automático personalizado utilizando uno de los métodos siguientes:

- Si es la primera vez que está añadiendo un proveedor de aprendizaje automático personalizado a {{site.data.keyword.aios_short}}, puede utilizar la interfaz de configuración. Para obtener más información, consulte [Especificación de una instancia de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Debe utilizar este método si desea tener más de un proveedor. Para obtener más información sobre cómo realizar esta acción mediante programación, consulte [Enlazar el motor de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Cuadernos de ejemplo
{: #frmwrks-custom-smpl-ntbks}

- [Creación del motor de aprendizaje automático personalizado utilizando el clúster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Creación de la despensa de datos, supervisión del despliegue del modelo y análisis de datos](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorar más
{: #frmwrks-custom-mediumblogs}

[Supervisar el motor de aprendizaje automático personalizado con Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
