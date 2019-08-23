---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure studio, ml, machine learning, services, studio

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

# Especificación de una instancia de Microsoft Azure ML Studio
{: #connect-azure}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de Microsoft Azure ML Studio. La instancia de Azure ML Studio es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de Microsoft Azure Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Conecte su instancia de Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de Azure ML Studio.

1. En la pestaña **Configurar**, pulse **Proveedor de aprendizaje automático**. En función de su entorno, es posible que no vea todos los proveedores siguientes:

   ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

1.  Pulse el mosaico **Microsoft Azure ML Studio**.

    ![Especificar credenciales de Azure ML Studio](images/connect-azure-cred.png)

1.  Especifique y guarde sus credenciales:

    - ID de cliente: el valor de serie real del ID de cliente, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Studio.
    - Secreto de cliente: el valor de serie real del secreto, que verifica quién es y autentica y autoriza las llamadas que realiza a Azure Studio.
    - Inquilino: el ID de inquilino correspondiente a su organización y que es una instancia dedicada de Azure AD. Para encontrar el ID de inquilino, pase el puntero del ratón por el nombre de cuenta para obtener el ID de inquilino o directorio, o bien seleccione Azure Active Directory > Propiedades > ID de directorio en el portal de Azure.
    - ID de suscripción: las credenciales de suscripción identifican de forma exclusiva su suscripción de Microsoft Azure. El ID de suscripción forma parte del URI para cada llamada de servicio.
    - Nombre de instancia de proveedor de servicio: el nombre específico asignado a este proveedor de servicio.
    - Descripción: (opcional) la descripción en lenguaje sencillo de esta instancia de proveedor de servicio. Si no tiene entornos de producción y de prueba, este sería un buen lugar donde incluir esa información.


    Consulte [Cómo utilizar el
portal para crear una entidad de servicio y una aplicación de Azure AD que puedan acceder a recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para ver instrucciones sobre
cómo obtener sus credenciales de Microsoft Azure.
    {: note}

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar y pulse **Configurar**.

Ha seleccionado correctamente los despliegues.

### Pasos siguientes
{: #ca-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
