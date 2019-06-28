---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Creación de credenciales
{: #cred-create}

Para acceder a las API REST de {{site.data.keyword.aios_short}}, se requiere una clave de API de plataforma y un ID de despensa de datos (instancia de servicio). La clave de API de plataforma le proporciona a un usuario individual la capacidad de acceder a recursos en {{site.data.keyword.cloud_notm}}.

Para las cuentas empresariales, un administrador puede crear la despensa de datos e invitar a otros usuarios a la cuenta, proporcionándoles acceso a una despensa de datos específica de {{site.data.keyword.aios_short}}. A continuación, un usuario puede crear su propia clave de API de plataforma y acceder a la misma despensa de datos de {{site.data.keyword.aios_short}}; no hay ningún conflicto ni riesgo de seguridad.

Para crear una clave de API de plataforma, realice los pasos siguientes:

- Inicie sesión en [{{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window}.

- Seleccione **Gestionar** --> **Seguridad** --> **Claves de API de plataforma**

    ![Claves de API de plataforma](images/cred-api-key.png)

- Cree y guarde una clave de API de plataforma.

Para buscar su ID de despensa de datos (o instancia de servicio):

- En la página {{site.data.keyword.aios_short}} **Configuración --> Resumen**, la primera entrada es el ID de su despensa de datos (instancia de servicio).

    ![ID de despensa de datos](images/data-mart-id.png)
