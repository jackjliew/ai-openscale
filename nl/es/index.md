---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Acerca de
{: #in-ov}

{{site.data.keyword.aios_full}} es un entorno de clase empresarial para aplicaciones que integran inteligencia artificial, que proporciona a las empresas visibilidad de cómo la inteligencia artificial crea, utiliza y proporciona rentabilidad, a nivel de su negocio.
{: shortdesc}

<p>&nbsp;</p>

## Implementación
{: #in-imp}

Así es cómo implementará {{site.data.keyword.aios_short}}:

- **Configure {{site.data.keyword.aios_short}}**: con el entorno gráfico de fácil utilización, [configure una base de datos de registro de carga útil](/docs/services/ai-openscale?topic=ai-openscale-connect-db) y la [instancia de Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) donde se almacenan los modelos y despliegues de inteligencia artificial.

- **Trabaje con supervisores**: para cada despliegue, configure cómo {{site.data.keyword.aios_short}} supervisará ese despliegue. Puede supervisar lo siguiente:

    - [Equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [Exactitud](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)

- **Visualice y edite los datos supervisados**: el {{site.data.keyword.aios_short}} [panel de control](/docs/services/ai-openscale?topic=ai-openscale-io-ov) le permite ver fácilmente los detalles clave e identificar problemas de sus despliegues. La visualización de puntos de datos individuales para cada característica supervisada proporciona detalles adicionales.

<p>&nbsp;</p>

## Limitaciones
{: #in-lim}

- El release actual sólo da soporte a una base de datos, una instancia de Watson Machine Learning y una instancia de {{site.data.keyword.aios_short}}

- La base de datos y la instancia de Watson Machine Learning se deben desplegar en la misma cuenta de {{site.data.keyword.cloud_notm}}.

- El plan Lite (gratuito) tiene los siguientes límites mensuales:

    - Dos modelos desplegados supervisados
    - 20 transacciones explicadas
    - 50.000 registros de carga útil (acumulativos)
    - 50.000 registros de opiniones (acumulativos)

- {{site.data.keyword.aios_short}} utiliza la base de datos PostgreSQL o Db2 para almacenar datos de salida o de reentrenamiento del despliegue de modelo. Actualmente no se da soporte a los planes Lite Db2.

- Hay un límite de licencias de 20 modelos desplegados por instancia de {{site.data.keyword.aios_short}}.

- Actualmente se pueden generar explicaciones para imágenes con un tamaño mayor de 1 MB.

<p>&nbsp;</p>


## Motores y infraestructuras de aprendizaje automático soportados
{: #in-fram}

El servicio {{site.data.keyword.aios_short}} da soporte a los siguientes motores de aprendizaje
automático. Cada tiempo de ejecución da soporte a los modelos creados en las infraestructuras siguientes:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personalizado](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Motor de aprendizaje automático de Google Cloud](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (solo ICP)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

El soporte completo incluye las siguientes características para la infraestructura, el problema y el tipo de datos específicos:

- Registro de carga útil	
- Registro de opiniones	
- Exactitud de rendimiento	
- Detección de sesgo en tiempo de ejecución	
- Explicabilidad	
- Eliminación automática de sesgo

<p>&nbsp;</p>

## Soporte de navegadores
{: #in-brw}

Las herramientas del servicio de {{site.data.keyword.aios_short}} requieren el mismo nivel de software del navegador que requiere {{site.data.keyword.cloud_notm}}. Consulte el tema {{site.data.keyword.cloud_notm}} [Requisitos previos](/docs/overview?topic=overview-prereqs-platform#browsers-platform) para obtener más detalles.

<p>&nbsp;</p>

## Herramienta de la CLI de ModelOps
{: #in-mop}

La herramienta de operaciones de modelo de CLI de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} le permite ejecutar tareas relacionadas con la gestión de ciclo de vida de los modelos de aprendizaje automático. Esta herramienta es complementaria de la herramienta de CLI de {{site.data.keyword.cloud_notm}}, aumentada con el [plugin de aprendizaje automático ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

<p>&nbsp;</p>

## Cliente Python
{: #in-pyc}

El cliente Python de [{{site.data.keyword.aios_short}} ![Incono de enlace externo](../../icons/launch-glyph.svg "Incono de enlace externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window} es una biblioteca Python que le permite trabajar directamente con el servicio de {{site.data.keyword.aios_short}} en {{site.data.keyword.cloud_notm}}. Puede utilizar el cliente Python, en lugar de la interfaz de usuario de cliente de {{site.data.keyword.aios_short}}, para configurar directamente una base de datos de registro, enlazar el motor de aprendizaje automático y seleccionar y supervisar despliegues. Para ver ejemplos de esta utilización del cliente Python, consulte los cuadernos de ejemplo de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Pasos siguientes
{: #in-next}

- [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) con el servicio.
- Vea el [Material de referencia de la API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

¿Todavía tiene dudas? [Póngase en contacto con IBM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
