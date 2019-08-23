---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Especificación de una instancia de servicio de Amazon SageMaker ML
{: #csm-connect}

El primer paso en la herramienta {{site.data.keyword.aios_short}} es especificar una instancia de servicio de Amazon SageMaker. La instancia de servicio de Amazon SageMaker es dónde se almacenan los modelos y despliegues de inteligencia artificial.
{: shortdesc}

También puede añadir el proveedor de aprendizaje automático utilizando el SDK de Python. Para obtener más información sobre cómo hacer esto programáticamente, consulte [Enlazar el motor de aprendizaje automático de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Conecte su instancia de servicio de Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} se conecta a modelos y despliegues de inteligencia artificial en una instancia de servicio de Amazon SageMaker.

1. En la pestaña **Configurar**, pulse **Proveedor de aprendizaje automático**. En función de su entorno, es posible que no vea todos los proveedores siguientes:

   ![Se muestra la pantalla Seleccionar el proveedor de servicio de aprendizaje automático con mosaicos para los motores de aprendizaje automático soportados](images/wos-machine-learning-providers-selection.png)

1.  Pulse el mosaico **Amazon SageMaker**.

    ![Especificar las credenciales de servicio de Amazon SageMaker](images/connect-sage-cred.png)

1.  Especifique y guarde sus credenciales:

    - ID de clave de acceso: el ID de clave de acceso de AWS, `aws_access_key_id`, que verifica quién es y autentica y autoriza las llamadas que realiza a AWS.
    - Clave de acceso secreta: su clave de acceso secreta de AWS, `aws_secret_access_key`, que se requiere para verificar quién es y para autenticar y autorizar las llamadas que realiza a AWS.
    - Región: especifique la región donde se ha creado su ID de clave de acceso. Las claves se almacenan y utilizan en la región en la que se han creado y no se pueden transferir a otra región. 
    - Nombre de instancia de proveedor de servicio: el nombre específico asignado a este proveedor de servicio.
    - Descripción: (opcional) la descripción en lenguaje sencillo de esta instancia de proveedor de servicio. Si no tiene entornos de producción y de prueba, este sería un buen lugar donde incluir esa información.

1.  {{site.data.keyword.aios_short}} lista sus modelos desplegados; seleccione los que desee supervisar.

### Pasos siguientes
{: #csm-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
