---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

Puede utilizar {{site.data.keyword.pm_full}} para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} da completo soporte a las siguientes infraestructuras de {{site.data.keyword.pm_full}}: 
{: shortdesc}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| Apache Spark MLlib | Clasificación | Estructurados |
| Apache Spark MLLib | Regresión | Estructurados |
| Keras con TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Clasificación | Desestructurado (imagen, texto) |
| Keras con TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Regresión | Desestructurado (imagen, texto) |
| Función de Python | Clasificación | Estructurados |
| Función de Python | Regresión | Estructurados |
| scikit-learn | Clasificación | Estructurados |
| scikit-learn | Regresión | Estructurados |
| XGBoost | Clasificación | Estructurados |
| XGBoost | Regresión | Estructurados |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

<sup>1</sup>El soporte de Keras no incluye el soporte de la equidad.
{: note}

<sup>2</sup>Se da soporte a la explicabilidad si el modelo o la infraestructura genera probabilidades de predicción.
{: note}

## Especificación de una instancia de servicio de {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de {{site.data.keyword.pm_full}}. La instancia de {{site.data.keyword.pm_short}} es donde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

### Requisitos previos
{: #wml-prereq}

Debe haber suministrado una instancia de {{site.data.keyword.pm_full}} en la misma cuenta de {{site.data.keyword.Bluemix_notm}} donde
está presente la instancia de servicio de {{site.data.keyword.aios_short}}. Si ha proporcionado una instancia de {{site.data.keyword.pm_full}} en alguna otra cuenta, no
podrá configurar dicha instancia con registro de carga útil automático con {{site.data.keyword.aios_short}}.

### Conecte su instancia de servicio de {{site.data.keyword.pm_short}}
{: #wml-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de {{site.data.keyword.pm_full}}.

1.  En la pestaña **Configurar**, en el panel de navegación, pulse **Proveedores de aprendizaje automático**.

    ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

2.  Pulse el botón **Añadir proveedor de aprendizaje automático** y, a continuación, pulse el mosaico {{site.data.keyword.pm_full}}. {{site.data.keyword.aios_short}} comprueba la cuenta de {{site.data.keyword.Bluemix_notm}} para localizar las instancias de
{{site.data.keyword.pm_full}} existentes. 
3. Seleccione una instancia en el menú desplegable **Watson Machine Learning service**.

    ![Seleccionar servicio de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Opcional) También tiene la opción de **Seleccionar otra ubicación**, para especificar una ubicación de aprendizaje automático fuera de su cuenta de {{site.data.keyword.Bluemix_notm}}. Proporcione credenciales para la ubicación como JSON válido:

    ![Establecer instancia de {{site.data.keyword.pm_short}}](images/gs-get-wml.png)

    Pulse **Guardar**.

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar y pulse **Configurar**.

## Pasos siguientes
{: #wml-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
