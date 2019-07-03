---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits

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

# Motores, infraestructuras y modelos de aprendizaje automático soportados
{: #in-fram}

El servicio {{site.data.keyword.aios_short}} da soporte a los siguientes motores de aprendizaje
automático. Cada tiempo de ejecución da soporte a los modelos creados en las infraestructuras siguientes:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Personalizado](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (solo disponible en
{{site.data.keyword.wos4d_full}})

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Motor de aprendizaje automático de Google Cloud](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

El soporte completo incluye las siguientes características para la infraestructura, el problema y el tipo de datos específicos:

- Registro de carga útil	
- Registro de opiniones	
- Exactitud de rendimiento	
- Detección de sesgo en tiempo de ejecución	
- Explicabilidad	
- Eliminación automática de sesgo

<p>&nbsp;</p>


## Tipos de modelos soportados
{: #abt-models}

Tabla 1. Detalles de soporte de modelo

| Algoritmos | **Equidad** | **Eliminación automática de sesgo** | **Explicar** | **Exactitud** |
|:---|:---:|:---:|:---:|:---:|
| **Clasificación estructurada** | Sí | Sí<sup>1</sup> | Sí<sup>1</sup> | Sí |
| **Regresión estructurada**     | Sí | Próximamente | Sí | Sí |
| **Clasificación de texto**       | No - tema de investigación activa | No - tema de investigación activa | Sí<sup>1</sup> | No |
| **Clasificación de imagen**      | No - tema de investigación activa | No - tema de investigación activa | Sí<sup>1</sup> | No ||
{: caption="Detalles de soporte del modelo" caption-side="top"}

<sup>1</sup> Si el modelo / la infraestructura genera como salida probabilidades de predicción

<p>&nbsp;</p>

## Soporte de navegadores
{: #in-brw}

Las herramientas del servicio de {{site.data.keyword.aios_short}} requieren el mismo nivel de software del navegador que requiere {{site.data.keyword.cloud_notm}}. Consulte el tema {{site.data.keyword.cloud_notm}} [Requisitos previos](/docs/overview?topic=overview-prereqs-platform#browsers-platform) para obtener más detalles.

<p>&nbsp;</p>

## Herramienta de la CLI de ModelOps
{: #in-mop}

La [herramienta de operaciones de modelo de CLI de {{site.data.keyword.aios_short}}](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external} le permite ejecutar tareas relacionadas con la gestión de ciclo de vida de modelos de aprendizaje automático. Esta herramienta es complementaria a la herramienta CLI de {{site.data.keyword.cloud_notm}}, aumentada con el [plugin de aprendizaje automático](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

## Cliente Python
{: #in-pyc}

El [cliente de Python de {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} es una biblioteca de Python que le permite trabajar directamente con el servicio de {{site.data.keyword.aios_short}} en {{site.data.keyword.cloud_notm}}. Puede
utilizar el cliente Python, en lugar de la interfaz de usuario de cliente de {{site.data.keyword.aios_short}}, para configurar directamente una
base de datos de registro, enlazar el motor de aprendizaje automático y seleccionar y supervisar despliegues. Para ver los ejemplos que
utilizan el cliente de Python de esta forma, consulte los [cuadernos
de ejemplo de {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Pasos siguientes
{: #in-next}

- [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) con el servicio.
- Vea el [material de referencia de API](https://{DomainName}/apidocs/ai-openscale){: external}.

¿Todavía tiene dudas? 

- [Novedades](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contactar con IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
