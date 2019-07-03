---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Roles y acciones de Identity and Access Management

El acceso a las instancias de servicio de {{site.data.keyword.aios_full}} para los usuarios de la cuenta lo controla {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Todos los usuarios que acceden al servicio de {{site.data.keyword.aios_short}} en su cuenta deben tener asignada una política de acceso con un rol de IAM definido. La política determina qué acciones puede llevar a cabo un usuario en el contexto del servicio o la instancia que seleccione. Las acciones permitidas se personalizan y definen mediante el servicio {{site.data.keyword.Bluemix_notm}} como operaciones que se permite que se realicen en el servicio. A continuación, las acciones se correlacionan con los roles de usuario de IAM.

Las políticas permiten que se otorgue acceso en distintos niveles. Algunas de las opciones son las siguientes: 

* Acceso a todas las instancias del servicio de su cuenta
* Acceso a una instancia de servicio individual en su cuenta
* Acceso a un recurso específico dentro de una instancia

Después de definir el ámbito de la política de acceso, se asigna un rol que determina el nivel de acceso del usuario. Revise las tablas siguientes que describen las acciones que cada rol permite en el servicio de {{site.data.keyword.aios_short}}.

En la tabla siguiente se detallan las acciones que se correlacionan con los roles de gestión de plataforma. Los roles de gestión de plataforma permiten a los usuarios realizar tareas en los recursos de servicio a nivel de plataforma, por ejemplo, asignar acceso de usuario para el servicio, crear o suprimir instancias y enlazar instancias a las aplicaciones.

|Rol de gestión de plataforma |Descripción de acciones | Acciones de ejemplo |
|--------------------------|------------------------|-----------------------------------------------------------------|
|Visor                       | Descripción            | <ul><li>  Ejemplo 1</li><li>Ejemplo 2</li></ul>                   |
|Editor                      | Descripción              |<ul><li>Ejemplo 1</li><li>Ejemplo 2</li></ul>                    |
|Operador                    | Descripción              | <ul><li>Ejemplo 1</li><li>Ejemplo 2</li><li>Ejemplo 3</li></ul> |
|Administrador               | Descripción              |<ul><li>Ejemplo 1</li><li>Ejemplo 2</li><li>Ejemplo 3</li></ul>  |
{: caption="Tabla 1. Roles de usuario y acciones de IAM" caption-side="top"}


En la tabla siguiente se detallan las acciones que se correlacionan con los roles de acceso al servicio. Los roles de acceso al servicio permiten a los usuarios acceder a {{site.data.keyword.aios_short}} así como a la posibilidad de llamar a la API de {{site.data.keyword.aios_short}}.

| Rol de acceso al servicio |Descripción de acciones | Acciones de ejemplo |
|---------------------|------------------------|-----------------------------------------------------------------|
|Lector                    | Descripción              | <ul><li>Ejemplo 1</li><li>Ejemplo 2</li></ul>                   |
|Escritor                  | Descripción              |<ul><li>Ejemplo 1</li><li>Ejemplo 2</li></ul>                    |
|Gestor                    | Descripción              | <ul><li>Ejemplo 1</li><li>Ejemplo 2</li><li>Ejemplo 3</li></ul> |
{: caption="Tabla 2. Roles y acciones de acceso al servicio de IAM" caption-side="top"}


Para obtener información sobre la asignación de roles de usuario en la interfaz de usuario, consulte [Gestión del acceso a los recursos](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
