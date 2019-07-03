---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: release notes, what's new 

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

# Novedades
{: #rn-relnotes}

En este documento se describen las características nuevas de {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 11 de junio de 2019
{: #rn-11June2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

- __*Funcionalidad del panel de control actualizado*__: El panel de control de {{site.data.keyword.aios_short}} ha sido sometido a varias revisiones. Esta nueva versión contiene las mejoras siguientes:

    - Un nuevo panel de ayuda facilita encontrar recursos, tales como StackOverflow, soporte de IBM y 
    - Se ha habilitado la globalización para el panel de control
    - Mejoras en la capacidad de uso

## 7 de junio de 2019
{: #rn-7June2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

- __*Interfaz de línea de mandatos mejorada*__: la interfaz de línea de mandatos, ibm-ai-openscale-cli, se ha actualizado y se ha liberado ahora la versión 0.2.148. Esta nueva versión contiene las mejoras siguientes:

    - Se ha actualizado el historial de métricas de calidad para incluir la gama completa de nuevas métricas de calidad soportadas por OpenScale
    - Soporte para la especificación de un certificado SSL directamente cuando se utiliza IBM DB2
    - Soporte para el nuevo SDK de Python ibm-ai-openscale 2.1.8
    - Otras correcciones de errores y mejoras de la estabilidad

   Instale desde PyPI ejecutando el mandato `pip install -U ibm-ai-openscale-cli` y obtenga ayuda sobre el uso ejecutando el mandato `ibm-ai-openscale-cli --help`. Para obtener más información, consulte la [página de proyectos de PyPI](https://pypi.org/project/ibm-ai-openscale-cli).

## 29 de mayo de 2019
{: #rn-29May2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

- __*Bias Mejoras de la visualización del sesgo*__: ![etiqueta beta](images/beta.png) La visualización de sesgo incluye las vistas siguientes: 

    - Carga útil + Alterados: incluye la solicitud de puntuación recibida para la hora seleccionada más registros adicionales de las horas anteriores si no se cumple el número mínimo de registros necesarios para la evaluación. Incluye registros alterados/sintetizados adicionales utilizados para probar la respuesta del modelo cuando el valor de la característica supervisada cambia.
    - Carga útil: las solicitudes de puntuación reales recibidas por el modelo durante la hora seleccionada.
    - Entrenamiento: los registros de datos de entrenamiento utilizados para entrenar el modelo.
    - Sin sesgo: la salida del algoritmo sin sesgo tras procesar el tiempo de ejecución y los datos alterados.

   Para obtener más información, consulte [Visualización del sesgo](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Cálculo de la exactitud para salida sin sesgo*__: el cálculo de la exactitud incluye la salida sin sesgo. Puede comparar la exactitud del modelo sin sesgo con la exactitud de un modelo de producción

   Para obtener más información, consulte [Exactitud](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Soporte de varios motores de aprendizaje automático*__: {{site.data.keyword.aios_short}} da soporte a varios motores de aprendizaje automático en una única instancia siempre que el suministro se realice mediante el [SDK de Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).

   Para obtener más información, consulte [Soporte](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Soporte de la internacionalización*__: {{site.data.keyword.aios_short}} da soporte a versiones localizadas e incluye datos de proceso en los idiomas soportados. La interfaz de usuario, la documentación y los mensajes de error de {{site.data.keyword.aios_short}} actualmente están traducidos a los idiomas siguientes: 
    - Alemán
    - Francés
    - Italiano
    - Español
    - Portugués de Brasil
    - Japonés
    - Chino simplificado
    - Chino tradicional
    - Coreano

   Para obtener más información (incluidas las limitaciones), consulte [Idiomas soportados en {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __*Mejoras de la infraestructura de {{site.data.keyword.pm_full}}*__: {{site.data.keyword.aios_short}} ahora da soporte a las infraestructuras scikit-learn y XGBoost en el motor de {{site.data.keyword.pm_full}}.

   Para obtener más información, consulte [infraestructuras de {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25 de abril de 2019
{: #rn-25April2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

Además de las mejoras de usabilidad y las actualizaciones de seguridad, nuestros desarrolladores han estado ocupados con nuevas características. Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado durante las semanas anteriores incluyen, entre otras:

- __*Visita guiada de configuración automatizada*__: una manera de configurar el entorno de {{site.data.keyword.aios_short}} mediante una nueva visita guiada. Utilice la [Configuración automatizada](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) para suministrar servicios y descargar y configurar un modelo. Verá esta opción cuando tenga una instancia nueva de {{site.data.keyword.aios_short}}.
- __*Cambiar a beta*__: ![etiqueta beta](images/beta.png) un nuevo conmutador, **Explore la nueva versión beta**, le permite trabajar en nuestro entorno beta, donde puede consultar todas las últimas características y nuevas funciones. ¿No le gusta lo que ve? Simplemente vuelva a cambiar pulsando **Volver a la versión original**. Esto no afecta a la configuración ni a los supervisores. Las prestaciones siguientes forman parte del programa beta actual:
    - __*Confusion matrix*__: [Confusion Matrix muestra](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx) los falsos positivos y los falsos negativos. Pulse en una celda para ver el subconjunto de registros de opiniones.

## 10 de abril de 2019
{: #rn-10April2019}

- __*Ahora la herramienta Express Path da soporte a modelos de cliente*__: automatiza el proceso de incorporación en {{site.data.keyword.aios_short}}.

   Para obtener más información, consulte [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/).


## 5 de marzo de 2019
{: #rn-5March2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Nuevo modelo de riesgo crediticio*__: se da soporte a un nuevo ejemplo de modelo de riesgo crediticio/guía de aprendizaje para todos los motores de puntuación. Para obtener más información, consulte los temas [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) y [Recursos adicionales](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Cálculo de la eliminación del sesgo*__: puede conmutar entre el modelo de producción y el modelo del que se ha eliminado el sesgo creado por {{site.data.keyword.aios_short}}. Para obtener más información, consulte [Modelo de producción y modelo sin sesgo](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) y [Cómo funciona la eliminación del sesgo](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22 de febrero de 2019
{: #rn-22February2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Actualizaciones de la interfaz de usuario*__: puede importar un archivo JSON para configurar programáticamente todos los supervisores y características durante la creación de la suscripción. También puede exportar el archivo de configuración. Consulte el tema [Configurar suscripción de despliegue utilizando archivos JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) para obtener más información.

## 7 de febrero de 2019
{: #rn-7February2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Actualizaciones de la interfaz de usuario*__: se han realizado diversas mejoras en la interfaz de usuario de {{site.data.keyword.aios_short}}, incluida una manera de [comprobar la equidad y la exactitud bajo demanda](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), así como la posibilidad de ver una lista de transacciones desde el [gráfico de detalles de equidad](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Mejoras de la explicabilidad*__: ahora todos los números tienen la misma precisión/escala en los valores de Positivo pertinente (PP) y Negativo pertinente (NP).

- __*Soporte de Db2 SSL*__: {{site.data.keyword.aios_short}} permite pasar certificados autofirmados (codificados en Base-64) con credenciales de DB2.

- __Soporte de la base de datos *{{site.data.keyword.Bluemix}}*__: {{site.data.keyword.aios_short}} da soporte ahora a bases de datos para PostgreSQL, además de Compose for PostgreSQL y Db2)

## 14 de diciembre de 2018
{: #rn-14December2018}

Están disponibles los siguientes cambios, características nuevas y problemas conocidos en el servicio.

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release beta anterior:

- __*Disponibilidad general*__: El release de disponibilidad general (GA) de {{site.data.keyword.aios_full_notm}}
como plan Standard (de pago) de {{site.data.keyword.Bluemix}}.

- __*IBM Cloud Pak for Data V1.2*__: Si utiliza {{site.data.keyword.wos4d_full}} V1.2, consulte la
documentación, incluidas las instrucciones de instalación, aquí: [Lista de comprobación de instalación](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Soporte para el tipo de modelo*__: Además de los despliegues de modelos de inteligencia artificial en {{site.data.keyword.pm_full}}, {{site.data.keyword.aios_short}} da soporte a despliegues de modelos en Microsoft Azure, Amazon SageMaker y entornos personalizados. Consulte [Tipos de modelos soportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov) para obtener más información.

- __*Base de datos "lite" gratuita*__: una base de datos gestionada "lite" gratuita proporciona todo lo que necesita utilizando {{site.data.keyword.aios_short}}. Consulte los [planes de precios de {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} para obtener detalles.

- __*Supervisión del sesgo*__: Soporte de atributos protegidos de tipo `float` y
`double`, y detección de sesgo en modelos de regresión lineales. Y {{site.data.keyword.aios_short}} puede eliminar automáticamente el sesgo del modelo de inteligencia artificial. Consulte [Información sobre la equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) para obtener más información.

- __*Explicabilidad*__: Soporte de modelos de regresión, funciones Python y explicaciones contrastivas complementarias. Consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) para obtener más información.

- __*Almacén de datos*__: Supervisión de la calidad sin depender de {{site.data.keyword.pm_full}} y la
posibilidad de utilizar su propia base de datos, ya sea Db2, Postgres o Db2 on Cloud.

- __*Interfaz de usuario mejorada*__: La interfaz de usuario de {{site.data.keyword.aios_short}} se ha mejorado para incluir una distribución de histograma de tiempo de ejecución con conmutación para datos de entrenamiento, ID y versiones de modelo y una tabla de ID de transacciones desde el histograma. Consulte [Visualización de datos de una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obtener más información.

- __*Opción de configuración de guía de aprendizaje alternativa*__: Para automatizar el suministro y la configuración de los servicios necesarios de {{site.data.keyword.Bluemix}} y para ver una aplicación de IBM {{site.data.keyword.aios_full}}, incluidos los datos de ejemplo, puede instalar y ejecutar un módulo Pythone. Consulte [Instalación de un módulo Python para configurar {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 de septiembre de 2018
{: #rn-17September2018}

- **Release de versión preliminar beta**: bienvenido al release de versión preliminar beta de {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Pasos siguientes
{: #relnotes-in-next}

¿Todavía tiene dudas?

- [Limitaciones](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Problemas conocidos](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
