---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: release notes, what's new 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Novedades
{: #rn-relnotes}

En este documento se describen las características nuevas y los problemas conocidos de {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 25 de abril de 2019
{: #rn-25April2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

### Características nuevas y cambios
{: #rn-25April2019nf}

Además de las mejoras de usabilidad y las actualizaciones de seguridad, nuestros desarrolladores han estado ocupados con nuevas características. Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado durante las semanas anteriores incluyen, entre otras:

- __*Visita guiada de configuración automatizada*__: una manera de configurar el entorno de {{site.data.keyword.aios_short}} mediante una nueva visita guiada. Utilice la [Configuración automatizada](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) para suministrar servicios y descargar y configurar un modelo. Verá esta opción cuando tenga una instancia nueva de {{site.data.keyword.aios_short}}.
- __*Cambiar a beta*__: ![etiqueta beta](images/beta.png) un nuevo conmutador, **Explore la nueva versión beta**, le permite trabajar en nuestro entorno beta, donde puede consultar todas las últimas características y nuevas funciones. ¿No le gusta lo que ve? Simplemente vuelva a cambiar pulsando **Volver a la versión original**. Esto no afecta a la configuración ni a los supervisores. Las prestaciones siguientes forman parte del programa beta actual:
    - __*Confusion matrix*__: [Confusion Matrix muestra](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx#it-conf-mtx) los falsos positivos y los falsos negativos. Pulse en una celda para ver el subconjunto de registros de opiniones.

## 5 de marzo de 2019
{: #rn-5March2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

### Características nuevas y cambios
{: #rn-5March2019nf}

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Nuevo modelo de riesgo crediticio*__: se da soporte a un nuevo ejemplo de modelo de riesgo crediticio/guía de aprendizaje para todos los motores de puntuación. Para obtener más información, consulte los temas [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) y [Recursos adicionales](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Cálculo de la eliminación del sesgo*__: puede conmutar entre el modelo de producción y el modelo del que se ha eliminado el sesgo creado por {{site.data.keyword.aios_short}}. Para obtener más información, consulte [Modelo de producción y modelo sin sesgo](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) y [Cómo funciona la eliminación del sesgo](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

## 22 de febrero de 2019
{: #rn-22February2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

### Características nuevas y cambios
{: #rn-22February2019nf}

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Actualizaciones de la interfaz de usuario*__: puede importar un archivo JSON para configurar programáticamente todos los supervisores y características durante la creación de la suscripción. También puede exportar el archivo de configuración. Consulte el tema [Configurar suscripción de despliegue utilizando archivos JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) para obtener más información.

## 7 de febrero de 2019
{: #rn-7February2019}

Están disponibles los siguientes cambios y características nuevas en el servicio.

### Características nuevas y cambios
{: #rn-7February2019nf}

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release anterior incluyen:

- __*Actualizaciones de la interfaz de usuario*__: se han realizado diversas mejoras en la interfaz de usuario de {{site.data.keyword.aios_short}}, incluida una manera de [comprobar la equidad y la exactitud bajo demanda](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), así como la posibilidad de ver una lista de transacciones desde el [gráfico de detalles de equidad](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Mejoras de la explicabilidad*__: ahora todos los números tienen la misma exactitud/escala en los valores de Positivo pertinente (PP) y Negativo pertinente (NP).

- __*Soporte de Db2 SSL*__: {{site.data.keyword.aios_short}} permite pasar certificados autofirmados (codificados en Base-64) con credenciales de DB2.

- __*Soporte de IBM Cloud Database*__: ahora {{site.data.keyword.aios_short}} admite Databases for PostgreSQL, además de Compose for PostgreSQL y Db2)

### Problemas conocidos
{: #rn-7February2019ki}

- **Instancia de servicio de Machine Learning personalizado**

    - El [módulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) actualmente no tiene Explicabilidad operativa para la instancia de servicio personalizado. Esto se debe a que la instancia de servicio personalizado requiere una predicción numérica en los datos de respuesta, que no se incluye con el script de módulo.

## 14 de diciembre de 2018
{: #rn-14December2018}

Están disponibles los siguientes cambios, características nuevas y problemas conocidos en el servicio.

### Características nuevas y cambios
{: #rn-12nf}

Las características de {{site.data.keyword.aios_short}} que se han añadido o mejorado desde el release beta anterior:

- __*Disponibilidad general*__: el release de disponibilidad general (GA) de {{site.data.keyword.aios_full_notm}} como plan Standard (de pago) de IBM Cloud.

- __*IBM Cloud Private for Data V1.2*__: si utiliza {{site.data.keyword.aios_short}} en IBM Cloud Private for Data V1.2, consulte la documentación, incluidas las instrucciones de instalación, aquí: [Lista de comprobación de instalación](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Soporte para el tipo de modelo*__: además de los despliegues de modelo de inteligencia artificial en Watson Machine Learning, {{site.data.keyword.aios_short}} admite despliegues de modelo en entornos de Microsoft Azure, Amazon SageMaker y personalizados. Consulte [Tipos de modelos soportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov) para obtener más información.

- __*Base de datos "lite" gratuita*__: una base de datos gestionada "lite" gratuita proporciona todo lo que necesita utilizando {{site.data.keyword.aios_short}}. Consulte los planes de precios de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/watson-openscale){: new_window} para ver más detalles.

- __*Supervisión del sesgo*__: soporte de atributos protegidos de tipo `float` y `double`, y detección de sesgo en modelos de regresión lineales. Y {{site.data.keyword.aios_short}} puede eliminar automáticamente el sesgo del modelo de inteligencia artificial. Consulte [Información sobre la equidad](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) para obtener más información.

- __*Explicabilidad*__: soporte de modelos de regresión, funciones Python y explicaciones contrastivas complementarias. Consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) para obtener más información.

- __*Almacén de datos*__: supervisión de la calidad sin depender de Watson Machine Learning, y posibilidad de utilizar su propia base de datos, ya sea Db2, Postgres o Db2 on Cloud.

- __*Interfaz de usuario mejorada*__: la interfaz de usuario de {{site.data.keyword.aios_short}} se ha mejorado para incluir una distribución de histograma de tiempo de ejecución con conmutación para datos de entrenamiento, ID y versiones de modelo y una tabla de ID de transacciones desde el histograma. Consulte [Visualización de datos de una hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obtener más información.

- __*Opción de configuración de guía de aprendizaje alternativa*__: para automatizar el suministro y la configuración de los servicios de IBM Cloud necesarios, y para ver una aplicación IBM {{site.data.keyword.aios_full}}, incluidos datos de ejemplo, puede instalar y ejecutar un módulo Python. Consulte [Instalación de un módulo Python para configurar {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

### Problemas conocidos
{: #rn-12ki}

- **Microsoft Azure**

    - De los dos tipos de servicios web de Azure Machine Learning, {{site.data.keyword.aios_short}} sólo admite el tipo `Nuevo`. El tipo `Clásico` no se admite.

    - __*Se debe utilizar el nombre de entrada predeterminado*__: en el servicio web de Azure, el nombre de entrada predeterminado es `"input1"`. Actualmente, este campo se establece para {{site.data.keyword.aios_short}} y, si falta, {{site.data.keyword.aios_short}} no funcionará.

      Si el servicio web de Azure no utiliza el nombre predeterminado, cambie el nombre de campo de entrada a `"input1"` y el código funcionará.

- **AWS SageMaker**

    - __*No se da soporte al algoritmo BlazingText*__: en el release actual de {{site.data.keyword.aios_short}}, no se da soporte al formato de carga útil de entrada de algoritmo BlazingText de AWS SageMaker.

## 17 de septiembre de 2018
{: #rn-17September2018}

### Características nuevas y cambios
{: #rn-17nf}

- **Release de versión preliminar beta**: bienvenido al release de versión preliminar beta de {{site.data.keyword.aios_full_notm}}.
