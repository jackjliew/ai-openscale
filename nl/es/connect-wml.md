---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Especificación de una instancia de servicio de Watson Machine Learning
{: #wml-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de Watson Machine Learning (WML). La instancia de WML es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Requisitos previos
{: #wml-prereq}

Debe haber suministrado una instancia de WML en la misma cuenta de {{site.data.keyword.Bluemix_notm}} donde está presente la instancia de servicio de {{site.data.keyword.aios_short}}. Si ha proporcionado una instancia de WML en alguna otra cuenta, no podrá configurar dicha instancia con {{site.data.keyword.aios_short}}.

## Conecte su instancia de servicio de Watson Machine Learning
{: #wml-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de WML.

1.  En la página de inicio de la herramienta {{site.data.keyword.aios_short}}, pulse **Empezar**.

    ![Página de inicio](images/gs-config-start.png)

2.  Seleccione el mosaico de Watson Machine Learning.

    ![Selección de mosaico](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} comprueba su cuenta de {{site.data.keyword.Bluemix_notm}} para localizar las instancias de WML existentes. A continuación, puede seleccionar una instancia en el menú desplegable **Servicio de Watson Machine Learning**.

    ![Seleccionar servicio de WML](images/gs-set-wml.png)

4.  (Opcional) También tiene la opción de **Seleccionar otra ubicación**, para especificar una ubicación de aprendizaje automático fuera de su cuenta de {{site.data.keyword.Bluemix_notm}}. Proporcione credenciales para la ubicación como JSON válido:

    ![Establecer instancia de WML](images/gs-get-wml.png)

    Pulse **Siguiente**.

5.  {{site.data.keyword.aios_short}} compruebe la instancia de Machine Learning para localizar la lista de despliegues almacenados en esa instancia. En la lista de despliegues, seleccione los que desee supervisar.

    ![Seleccionar despliegues](images/gs-config-deploy.png)

6.  Pulse **Siguiente**.
7.  Pulse **Guardar**.

### Pasos siguientes
{: #wml-next}

{{site.data.keyword.aios_short}} ahora está listo para que usted [especifique una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
