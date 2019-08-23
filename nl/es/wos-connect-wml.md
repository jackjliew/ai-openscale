---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Especificación de una instancia de servicio de {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de {{site.data.keyword.pm_full}}. La instancia de {{site.data.keyword.pm_short}} es donde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Requisitos previos
{: #wml-prereq}

Debe haber suministrado una instancia de {{site.data.keyword.pm_full}} en la misma cuenta de {{site.data.keyword.Bluemix_notm}} donde
está presente la instancia de servicio de {{site.data.keyword.aios_short}}. Si ha proporcionado una instancia de {{site.data.keyword.pm_full}} en alguna otra cuenta, no
podrá configurar dicha instancia con registro de carga útil automático con {{site.data.keyword.aios_short}}.

## Conecte su instancia de servicio de {{site.data.keyword.pm_short}}
{: #wml-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de {{site.data.keyword.pm_full}}.

1.  En la pestaña **Configurar**, pulse **Proveedor de aprendizaje automático**.

    ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

2.  Seleccione el mosaico de {{site.data.keyword.pm_full}}. {{site.data.keyword.aios_short}} comprueba la cuenta de {{site.data.keyword.Bluemix_notm}} para localizar las instancias de
{{site.data.keyword.pm_full}} existentes. 
3. Seleccione una instancia en el menú desplegable **Watson Machine Learning service**.

    ![Seleccionar servicio de {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Opcional) También tiene la opción de **Seleccionar otra ubicación**, para especificar una ubicación de aprendizaje automático fuera de su cuenta de {{site.data.keyword.Bluemix_notm}}. Proporcione credenciales para la ubicación como JSON válido:

    ![Establecer instancia de {{site.data.keyword.pm_short}}](images/gs-get-wml.png)

    Pulse **Guardar**.

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar y pulse **Configurar**.

### Pasos siguientes
{: #wml-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
