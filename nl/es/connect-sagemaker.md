---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

1.  En la página de inicio de la herramienta {{site.data.keyword.aios_short}}, pulse **Empezar**.

    ![Página de inicio](images/gs-config-start.png)

1.  Seleccione el titulo **Amazon SageMaker** y pulse **Siguiente**.

    ![Seleccionar servicio de Amazon SageMaker](images/connect-sage.png)

1.  Especifique sus credenciales:

    - ID de clave de acceso: el ID de clave de acceso de AWS, `aws_access_key_id`, que verifica quién es y autentica y autoriza las llamadas que realiza a AWS.
    - Clave de acceso secreta: su clave de acceso secreta de AWS, `aws_secret_access_key`, que se requiere para verificar quién es y para autenticar y autorizar las llamadas que realiza a AWS.
    - Región: especifique la región donde se ha creado su ID de clave de acceso. Las claves se almacenan y utilizan en la región en la que se han creado y no se pueden transferir a otra región. 

    ![Especificar las credenciales de servicio de Amazon SageMaker](images/connect-sage-cred.png)

1.  Pulse **Siguiente**.

1.  {{site.data.keyword.aios_short}} listará sus modelos desplegados; seleccione los que desee supervisar.

    ![Seleccionar modelos desplegados de Amazon SageMaker](images/connect-sage-deploys.png)

1.  Pulse **Siguiente**.

### Pasos siguientes
{: #csm-next}

{{site.data.keyword.aios_short}} ahora está listo para que usted [especifique una base de datos](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
