---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Microsoft Azure, ml, machine learning, services

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

# Especificación de una instancia de Microsoft Azure ML Studio
{: #connect-azure}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de Microsoft Azure ML Studio. La instancia de Azure ML Studio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

## Conecte su instancia de Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de Azure ML Studio.

1.  En la página de inicio de la herramienta {{site.data.keyword.aios_short}}, pulse **Empezar**.

    ![Página de inicio](images/gs-config-start.png)

1.  Seleccione el mosaico **Microsoft Azure ML Studio** y pulse **Siguiente**.

    ![Seleccionar Azure ML Studio](images/connect-azure.png)

1.  Especifique sus credenciales:

    Consulte [Cómo utilizar el portal para crear un principal de servicio y aplicación Azure AD que puedan acceder a recursos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window} para ver instrucciones sobre cómo obtener sus credenciales de Microsoft Azure.
    {: note}

    ![Especificar credenciales de Azure ML Studio](images/connect-azure-cred.png)

1.  Pulse **Siguiente**.

1.  {{site.data.keyword.aios_short}} listará sus modelos desplegados; seleccione los que desee supervisar.

    ![Seleccionar modelos desplegados de MS Azure](images/connect-azure-deploys.png)

1.  Pulse **Siguiente**.

### Pasos siguientes
{: #ca-next}

{{site.data.keyword.aios_short}} ahora está listo para que usted [especifique su base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
