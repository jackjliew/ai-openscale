---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navegación en el panel de control
{: #io-ov}

Puede realizar un seguimiento de todos los despliegues que está supervisando mediante el panel de control de {{site.data.keyword.aios_short}}. El panel de control es la vista principal de {{site.data.keyword.aios_short}}. El panel de instrumentos consta de cinco pestañas:

  ![Pestañas Detalles](images/insight-tabs.png)

{: shortdesc}

## Detalles
{: #io-ins}

La pestaña **Detalles** (![Panel de control Detalles](images/insight-dash-tab.png)) proporciona una vista de alto nivel de su supervisión del despliegue.

  ![Panel de control Detalles](images/insight-dashboard.png)

- ***Despliegues supervisados***: en este ejemplo, se supervisan un total de 10 despliegues. Ocho de los diez despliegues se muestran como mosaicos individuales a continuación.

- ***Alertas de Exactitud***: en los mosaicos siguientes se representan un total de 3 alertas de Exactitud con sombreado púrpura. En este ejemplo, los despliegues `Rendimiento de controlador`, `Análisis de mercado` y `Riesgo de precios` muestran los valores de Exactitud de `60%`, `65%` y `79%`, respectivamente.

- ***Alertas de Equidad***: en los mosaicos siguientes hay un total de 6 alertas de Equidad, representadas con sombreado púrpura y con una pequeña etiqueta `BIAS`. En este ejemplo, los despliegues `Rendimiento de controlador`, `Análisis de mercado`, `Conformidad normativa`, `Detección de fraudes`, `Optimización Premium` y `Estimación de coste de daños` muestran valores de Equidad de `59%`, `68%`, `62%`, `64%`, `79%` y `63%`, respectivamente.

Cada mosaico proporciona un resumen de la actividad de supervisión para ese despliegue. Observe que el despliegue `Direccionamiento de centro de llamadas` no muestra ningún problema, lo que indica un modelo preciso y considerablemente estable.

### Pasos siguientes
{: #io-next}

Seleccione cualquiera de los mosaicos de despliegue individuales para ver más detalles sobre ese despliegue. Para obtener información,
consulte [Supervisión de la equidad, solicitudes promedio por minuto y exactitud](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
y [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Configuración
{: #io-conf}

La pestaña **Configurar** (![Pestaña Configurar](images/insight-config-tab.png)) abre un Resumen de configuración para el despliegue seleccionado.

  ![Resumen de configuración](images/insight-config-summary.png)

Desde aquí, puede editar directamente los valores de configuración para el supervisor de despliegue.

## Transacciones
{: #io-tran}

Utilice la pestaña **Explicar una transacción** (![pestaña Explicar una transacción](images/insight-transact-tab.png)) para buscar un ID de transacción específico para explicar una transacción de despliegue determinada. Para obtener más información, consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Herramientas de IA
{: #io-too}

Utilice la pestaña **Herramientas de IA** (![pestaña Herramientas de IA](images/aitools.png)) para abrir herramientas y opciones de IA de IBM adicionales.

- *[El plan Lite Watson Studio Lite ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: Watson Studio
le ofrece el entorno y las herramientas para analizar y visualizar los datos, para depurar y dar forma a los datos, para consumir
datos en streaming, o para crear, entrenar y desplegar modelos de aprendizaje automático. Pulse en el enlace
"Registrarse para el plan gratuito de Watson Studio Lite" para obtener Watson Studio.

## Pestaña Ayuda
{: #io-help}

La pestaña Ayuda ( ![Pestaña Ayuda](images/insight-help-tab.png)) proporciona información adicional para ayudarle a utilizar {{site.data.keyword.aios_short}}.
