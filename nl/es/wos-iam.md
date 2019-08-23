---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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

Con roles de gestión de plataforma, se puede asignar a los usuarios distintos niveles de permiso para realizar acciones de plataforma en la cuenta y en un servicio. Por ejemplo, los roles de gestión de plataforma que se asignan para los recursos de catálogo permiten a los usuarios realizar acciones como crear, suprimir, editar y ver instancias de servicio. Además, los roles de gestión de plataforma que se asignan para los servicios de gestión de cuentas permiten a los usuarios realizar acciones tales como invitar y eliminar usuarios, trabajar con grupos de recursos y ver información de facturación. Para obtener más información acerca de los servicios de gestión de cuentas, consulte [Asignación de roles a los servicios de gestión de cuentas](/docs/iam?topic=iam-account-services#account-services){: external}.

Seleccione todos los roles aplicables al crear una política. Cada rol permite completar acciones individuales y no hereda las acciones de los roles inferiores.
{: tip}

En la tabla siguiente se proporcionan ejemplos para algunas de las acciones de gestión de plataforma que los usuarios pueden llevar a cabo en el contexto de recursos de catálogo y grupos de recursos. Consulte la documentación de cada oferta del catálogo para saber cómo se aplican los roles a los usuarios en el contexto del servicio que está utilizando.


|  | Uno o todos los servicios habilitados de IAM | Servicio seleccionado en un grupo de recursos | Grupo de recursos seleccionado |
|:--------------|:------------|:-------------|:-------------|
| Rol Visor | Ver instancias, alias, enlaces y credenciales | Ver solo instancias especificadas en el grupo de recursos | Ver grupo de recursos |
| Rol Operador |  Ver instancias y gestionar alias, enlaces y credenciales |  No aplicable | No aplicable |
| Rol Editor |  Crear, suprimir, editar y ver instancias. Gestionar alias, enlaces y credenciales | Crear, suprimir, editar, suspender, reanudar, ver y enlazar solo instancias especificadas en el grupo de recursos | Ver y editar el nombre de grupo de recursos |
| Rol Administrador |  Todas las acciones de gestión para los servicios | Todas las acciones de gestión para las instancias especificadas en el grupo de recursos | Ver, editar y gestionar el acceso para el grupo de recursos |
| Rol Administrador de clúster (específico de {{site.data.keyword.wos4d_full}} solamente) |  Tiene acceso completo a la plataforma IBM Cloud Private | Tiene acceso completo a las instancias específicas en el grupo de recursos | Únicamente el administrador de clúster puede completar las acciones siguientes: conectar a un directorio LDAP, añadir usuarios y asignarles los roles de IAM, gestionar cargas de trabajo, infraestructura y aplicaciones en todos los espacios de nombres, crear espacios de nombres, asignar cuotas, añadir políticas de seguridad de pod, añadir un repositorio Helm interno, suprimir un repositorio Helm interno, añadir gráficos Helm al repositorio Helm interno, eliminar gráficos Helm del repositorio Helm interno y sincronizar repositorios Helm internos y externos |
{: row-headers}
{: class="comparison-table"}
{: caption="Tabla 1. Ejemplos de roles y acciones de gestión de plataforma para servicios de una cuenta" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


Para los roles de acceso al servicio, que permiten a los usuarios acceder a {{site.data.keyword.aios_short}} así como llamar a la API REST, {{site.data.keyword.aios_short}} difiere de los roles de gestión de plataforma mostrados en la tabla anterior. Para obtener información sobre la asignación de roles de usuario en la interfaz de usuario, consulte [Gestión del acceso a los recursos](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}.

 
