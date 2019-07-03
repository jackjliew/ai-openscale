---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests

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

# Envío de una solicitud de puntuación
{: #cdb-score}

Para configurar supervisores, {{site.data.keyword.aios_short}} le solicita que envíe una carga útil de puntuación, para empezar a registrar los datos que se supervisarán.

- Para los modelos desplegados en {{site.data.keyword.pm_full}}, simplemente puntúe su despliegue. {{site.data.keyword.pm_short}} envía automáticamente la carga útil de puntuación a {{site.data.keyword.aios_short}}. 
- Para otros motores de aprendizaje automático, como Microsoft Azure, Amazon SageMaker o un motor de aprendizaje automático personalizado, se debe enviar la carga útil de puntuación utilizando la API de registro de carga útil. Para obtener más información, consulte [Registro de carga útil para instancias de servicio que no sean {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Puesto que {{site.data.keyword.aios_short}} puntúa automáticamente los modelos desplegados en {{site.data.keyword.pm_full}}, si sólo tiene modelos desplegados en {{site.data.keyword.pm_short}} aparece una marca de selección que indica que este paso se ha completado en la columna **Preparado para supervisar**.
{: note}

## Pasos para el registro de carga útil
{: #cdb-score-apisteps}

1. Seleccione un despliegue. En el ejemplo siguiente, el despliegue es **Detector de fraudes**.
2. Elija si desea utilizar el código `cURL` o `Python` pulsando la pestaña `cURL` o `Python`.
3. Pulse **Copiar en el portapapeles** y péguelo para registrar los datos de solicitud y respuesta de despliegue del modelo. Para obtener más información, consulte [Registro de carga útil para instancias de servicio que no sean {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Los campos y valores de los fragmentos de código se deben sustituir con sus valores reales, ya que los que se proporcionan son sólo ejemplos.
{: important}

![Seleccionar base de datos](images/config-send-scoring.png)

Una vez que ha ejecutado el registro de carga útil, aparecerá una marca de comprobación en la columna "Preparado para supervisar" para el despliegue seleccionado. Pulse **Configurar supervisores** para continuar.

## Información sobre el número de solicitudes de puntuación
{: #cdb-score-capacity}

Las solicitudes de puntuación son una parte integral del proceso de {{site.data.keyword.aios_short}}. Cada registro de transacción que envía al modelo que se va a puntuar genera un proceso adicional para que el servicio {{site.data.keyword.aios_short}} pueda realizar las perturbaciones y crear explicaciones.

- Para los modelos tabulares, de texto y de imagen, la siguiente solicitud de línea base genera puntos de datos:

   - 1 solicitud de puntuación genera 5000 puntos de datos.

- Sólo para los modelos de clasificación tabular, hay solicitudes de puntuación adicionales que se realizan para la explicación contrastiva. Se añaden las solicitudes siguientes a la solicitud de línea base anterior:

   - 100 solicitudes de puntuación generan 51 puntos de datos adicionales por solicitud.
   - 101 solicitudes de puntuación generan 1 punto de datos adicional por solicitud.


## Pasos siguientes
{: #cdb-score-next-steps-scoringreq}

[Configurar supervisores](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
