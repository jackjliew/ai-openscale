---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: Python, install, python module, setup, set up, insights, explainability

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

# Instalación de un módulo Python para configurar {{site.data.keyword.aios_short}}
{: #as-module}

Para automatizar el suministro y la configuración de los servicios necesarios de {{site.data.keyword.cloud_notm}} y ver una aplicación {{site.data.keyword.aios_full}}, incluidos los datos de ejemplo, puede instalar un módulo Python.
{: shortdesc}

## Acerca de este módulo
{: #as-about}

- El módulo proporciona a los usuarios técnicos una manera alternativa para ver una instancia de {{site.data.keyword.aios_short}} en ejecución sin necesidad de suministrar y configurar los servicios usted mismo, tal como se describe en la guía de aprendizaje [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted).
- El módulo Python ejecuta el proceso de comprobar los servicios de que dispone y de crear los servicios necesarios, incluido {{site.data.keyword.aios_short}}. Cuando el módulo se ha ejecutado correctamente, desde el panel de control de {{site.data.keyword.cloud_notm}} puede iniciar {{site.data.keyword.aios_short}} para ver cómo supervisa un modelo.

## Antes de empezar
{: #as-prereqs}

1. [Cree una clave de API de {{site.data.keyword.cloud_notm}} y descárguela](/docs/iam?topic=iam-userapikey#create_user_key). Necesitará especificar la clave de API en un paso posterior.

2. [Instale cualquier release de Python 3 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.python.org/downloads/){: new_window}.

  Python 3 incluye el sistema de gestión de paquetes pip necesario.
  {: note}

3. Instale el paquete `ibm-ai-openscale-cli` mediante el mandato siguiente:

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    Si hay varias versiones de pip instaladas en el sistema, es posible que deba ejecutar `pip3` y no `pip`, como en `pip3 install -U ibm-ai-openscale-cli`.
    {: tip}

4. Si tiene una instancia de servicio de {{site.data.keyword.pm_short}} existente, compruebe el panel de control de [{{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window} para asegurarse de que el servicio lo gestiona {{site.data.keyword.iamshort}} (IAM), no Cloud Foundry.

  **Importante**: El módulo comprueba si hay una instancia de {{site.data.keyword.pm_short}}. Si tiene una instancia, el módulo la utiliza. Sin embargo, si la instancia la gestiona Cloud Foundry, primero debe [migrarla a un grupo de recursos IAM antes de ejecutar el módulo](/docs/resources?topic=resources-migrate#migrate).

## Ejecución del módulo
{: #as-run}

Ejecute el mandato siguiente:

```
ibm-ai-openscale-cli --apikey <su clave de API>
```
{: codeblock}

## Visualización de los resultados en {{site.data.keyword.aios_short}}
{: #as-open}

Para ver los detalles de la equidad y la exactitud del modelo, detalles de los datos supervisados y la explicabilidad de una transacción individual, abra el panel de control de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}.

- Para comprender el escenario de los datos de ejemplo, lea [Caso de uso y el valor de {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use).

### Ver detalles
{: #as-insights}

En el panel de control de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, pulse la pestaña **Detalles**, que muestra una descripción general de las métricas para los modelos desplegados: ![Detalles](images/insight-dash-tab.png)

- La página Detalles muestra de un solo vistazo cualquier problema relacionado con la equidad y la exactitud, según determinan los umbrales configurados.

- Cada despliegue se muestra como un mosaico. El módulo ha configurado un despliegue denominado `GermanCreditRiskModel`, tal como se muestra en la siguiente captura de pantalla:

  ![Descripción general de Detalles](images/setup01-0206.png)

### Ver datos de supervisión
{: #as-monitoring}

1. En la página Detalles, pulse el mosaico `GermanCreditRiskModel` para ver detalles sobre los datos supervisados.
2. Deslice el marcador por el gráfico para ver un día y periodo de tiempo que muestren datos y, a continuación, pulse el enlace **Ver detalles**.

   - Por ejemplo, la pantalla siguiente muestra datos correspondientes a una fecha y hora específicas. Las fechas y las horas varían, en función de cuándo se ejecuta el módulo.

   - Para obtener información sobre cómo interpretar el gráfico de series de tiempo, consulte [Supervisión de la equidad, solicitudes promedio por minuto y exactitud](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

    ![Supervisar datos](images/setup02-0206.png)

3. Para ver detalles sobre la supervisión de datos de `EDAD`, asegúrese de que `EDAD` esté seleccionado en el menú desplegable.

  - Observe que en la siguiente captura de pantalla no existe ningún sesgo.

  - Para obtener información sobre cómo interpretar el gráfico de los puntos de datos a una hora específica, consulte [Supervisión de la equidad, solicitudes promedio por minuto y exactitud](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp).

    ![Ver detalles](images/setup03-0206.png)

### Ver explicabilidad
{: #as-explain}

Para comprender los factores que contribuyen a que haya un sesgo para un periodo de tiempo determinado, en la pantalla de visualización que se muestra en la sección anterior, seleccione el botón **Ver transacciones**.

Se listan los ID de transacción de la última hora correspondientes a las transacciones sesgadas. Para el modelo utilizado en este módulo, no existe ningún sesgo para las solicitudes disponibles. Por lo tanto, en la captura de pantalla siguiente no se muestran transacciones para el periodo de tiempo.

  ![Lista de transacciones sin transacciones](images/setup06-0206.png)

Para obtener información sobre cómo buscar y explicar transacciones, consulte [Explicación de las transacciones](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view).

## Información relacionada
{: #as-info}

- Para obtener información sobre sesgos, consulte [Equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
- Para obtener información sobre la exactitud con la que el modelo predice los resultados, consulte [Exactitud](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Para obtener información sobre cómo interpretar los gráficos y los datos, consulte [Supervisión de la equidad, solicitudes promedio por minuto y exactitud](/docs/services/ai-openscale?topic=ai-openscale-it-ov).
- Para obtener información sobre cómo los factores subyacentes influyen en los resultados, consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
