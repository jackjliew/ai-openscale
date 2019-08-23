---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API, datamart ID, IDs, binding ID,  deployment ID, subscription ID

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

# Creación de credenciales para {{site.data.keyword.aios_short}}
{: #cred-create}

Para acceder a las API REST de {{site.data.keyword.aios_full}}, se requiere una clave de API de plataforma y un ID de despensa de datos; los
ID son necesarios. La clave de API de plataforma le proporciona a un usuario individual la capacidad de acceder a recursos en {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Para cuentas empresariales, un administrador puede crear la despensa de datos, invitar a los usuarios a la cuenta y proporcionar acceso a una
despensa de datos específica de {{site.data.keyword.aios_short}}. A continuación, un usuario puede crear su propia clave de API de plataforma y
puede acceder a la misma despensa de datos de {{site.data.keyword.aios_short}}. No hay ningún riesgo de conflicto o de seguridad.

## Creación de la clave de API de la plataforma
{: #cred-create-apikey}

Para crear una clave de API de IBM Cloud, realice los pasos siguientes:

- Inicie sesión en [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}.
- Seleccione **Gestionar** --> **Acceso (IAM)** --> **Claves de API de {{site.data.keyword.cloud_notm}}**
- Pulse el botón **Crear una clave de API de IBM Cloud**.
- Dé a la clave un nombre y una descripción y pulse **Crear**.

## Búsqueda de ID de servicio:
{: #cred-find-datamart-id}

Busque los ID de despensa de datos, despliegue, suscripción o enlace, en la página {{site.data.keyword.aios_short}} **Registro de carga útil**, que se muestra al seleccionar **Configurar supervisores** para un despliegue.

1. Pulse el mosaico de despliegue del modelo. 
2. Pulse **Configurar supervisores** ![Icono Configurar](images/configure-deployment-button.png).
3. Pulse **Registro de carga útil**.
4. En la página **Registro de carga útil** de {{site.data.keyword.aios_short}}, en el panel **Detalles**, busque el ID que desea. Por ejemplo, el campo **ID de despensa de datos**:

    ![ID de despensa de datos](images/data-mart-id.png)

## Creación de credenciales de instancia de servicio mediante la consola de mandatos
{: #cred-creds}

Para crear las credenciales para {{site.data.keyword.aios_short}}, complete los pasos siguientes utilizando la [consola de mandatos](/docs/cli?){: external} de {{site.data.keyword.cloud_notm}}:

1. Recupere la clave de API ejecutando el mandato siguiente:

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    Aparecerá la siguiente información:

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```

2. Compruebe el grupo de recursos que utiliza en su cuenta de {{site.data.keyword.cloud_notm}}.

   1. Vaya al Panel de control.
   2. En el **Menú de navegación**, pulse **Lista de recursos**.
   3. En la columna **Grupo**, pulse la selección desplegable **Filtrar por grupo u organización** y establezca el recuadro de selección **Predeterminado**.

  ![Grupo de recursos en la nube](images/cloud-resource.png)

  Si no utiliza el grupo de recursos `Predeterminado`, ejecute el mandato siguiente para obtener sus credenciales para {{site.data.keyword.aios_short}}:

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  donde `myResourceGroup` es el nombre del grupo de recursos asociado con su instancia de {{site.data.keyword.aios_short}}.

3. Recupere el ID de instancia de {{site.data.keyword.aios_short}} ejecutando el mandato siguiente:

    ```curl
    ibmcloud resource service-instance '<Nombre_instancia__Watson_OpenScale>'
    ```

    **Nota**: Si utiliza la consola de mandatos de {{site.data.keyword.cloud_notm}} en Windows, sustituya las comillas simples
(') en los mandatos anteriores por comillas dobles (").

    Aparecerá la siguiente información:

    ```bash
    Nombre:                AI OpenScale-my_instance
    ID:                    crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Ubicación:             us-south
    Nombre de servicio:    aiopenscale
    Nombre plan servicio:  lite
    Nombre grupo recursos: Default
    Estado:                active
    Tipo:                  service_instance
    Subtipo:
    Etiquetas:
    Fecha de creación      2018-09-17T13:58:43Z
    Fecha actualización:
    ```

    El valor de `GUID` es su ID de instancia de {{site.data.keyword.aios_short}}.
        
## Pasos siguientes
{: #cred-create-next-steps}

Especifique el proveedor de aprendizaje automático:

- [Especificación de una instancia de servicio de IBM Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [Especificación de una instancia de Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [Especificación de una instancia de Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)
- [Especificación de una instancia de servicio de Amazon SageMaker ML](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [Especifique una instancia de servicio de Machine Learning personalizado](/docs/services/ai-openscale?topic=ai-openscale-co-connect)
