---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# Preguntas más frecuentes
{: #wos-faqs}

Aquí encontrará algunas de las preguntas más frecuentes de los usuarios de {{site.data.keyword.aios_full}}.
{: shortdesc}

## Preguntas
{: #wos-faqs-questions}

- [¿Qué es {{site.data.keyword.aios_short}}?](#faq-whatsa)
- [¿Qué precio tiene {{site.data.keyword.aios_short}}?](#faq-pricing)
- [¿Hay una versión de prueba gratuita de {{site.data.keyword.aios_short}}?](#faq-freetrial)
- [Todos mis modelos de inteligencia artificial se encuentran en Azure. ¿Puedo utilizar el motor de Microsoft Azure ML con {{site.data.keyword.aios_short}}?](#faq-azure)
- [Todos mis modelos de inteligencia artificial se encuentran en Amazon. ¿Puedo utilizar el motor de Amazon SageMaker ML con {{site.data.keyword.aios_short}}?](#faq-sagemaker)
- [¿Está {{site.data.keyword.aios_short}} disponible en {{site.data.keyword.icp4dfull_notm}}?](#faq-icp)
- [Quiero ejecutar {{site.data.keyword.aios_short}} en mis propios servidores. ¿Qué potencia de proceso informático debo asignar?](#faq-sizing)
- [¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?](#wos-faqs-convert-data-types)
- [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](#trainingdata)

### ¿Qué es {{site.data.keyword.aios_short}}?
{: #faq-whatsa}

Watson OpenScale realiza el seguimiento y la medición de los resultados de inteligencia artificial durante todo su ciclo de vida, y gobierna y adapta la inteligencia artificial a las cambiantes situaciones de negocio, para modelos creados y en ejecución en cualquier ubicación.

Vea este vídeo para obtener una descripción general rápida de {{site.data.keyword.aios_short}}.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Confianza y transparencia en la inteligencia artificial" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### ¿Qué precio tiene {{site.data.keyword.aios_short}}?
{: #faq-pricing}

Cuando esté listo para realizar la transición desde el plan Lite, hay un plan de precios **Estándar** que incluye la supervisión de hasta 24 modelos desplegados, sin restricciones en el número de carga útil, filas de opinión o transacciones para Explicabilidad. La información actualizada está disponible en el [catálogo de {{site.data.keyword.Bluemix}}](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}.


### ¿Hay una versión de prueba gratuita de {{site.data.keyword.aios_short}}?
{: #faq-freetrial}

{{site.data.keyword.aios_short}} ofrece una versión de prueba gratuita durante todo el plan Lite. Para registrarse, visite la [página web de {{site.data.keyword.aios_short}}](https://www.ibm.com/cloud/watson-openscale/){: external} y pulse **Get started now**. Podrá utilizar el plan Lite tanto tiempo como desee (sujeto a las limitaciones de uso mensual que se renuevan cada mes).

### Todos mis modelos de inteligencia artificial se encuentran en Azure. ¿Puedo utilizar el motor de Microsoft Azure ML con {{site.data.keyword.aios_short}}?
{: #faq-azure}

{{site.data.keyword.aios_short}} da soporte a los motores de Microsoft Azure ML Studio y de Microsoft Azure ML Service. Para obtener más información, consulte [Infraestructuras de Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure) e [Infraestructuras de Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service).

### Todos mis modelos de inteligencia artificial se encuentran en Amazon. ¿Puedo utilizar el motor de Amazon SageMaker ML con {{site.data.keyword.aios_short}}?
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} da soporte al motor de Amazon SageMaker ML. Para obtener más información, consulte [Infraestructuras de Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage).

### ¿Está {{site.data.keyword.aios_short}} disponible en {{site.data.keyword.icp4dfull_notm}}?
{: #faq-icp}

{{site.data.keyword.aios_short}} es uno de los complementos Premium de {{site.data.keyword.icp4dfull_notm}}. 

### Quiero ejecutar {{site.data.keyword.aios_short}} en mis propios servidores. ¿Qué potencia de proceso informático debo asignar?
{: #faq-sizing}

Hay directrices específicas para la [configuración de hardware](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt) para las configuraciones de tres y de seis nodos. El equipo de ventas técnicas de IBM puede ayudarle con el dimensionamiento de su configuración específica. Puesto que {{site.data.keyword.aios_short}} se ejecuta como un complemento de {{site.data.keyword.icp4dfull_notm}}, debe tener en cuenta los requisitos de ambos productos de software.

### ¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?
{: #wos-faqs-convert-data-types}

Al configurar la supervisión de la equidad para un modelo, la columna de predicción sólo permite un valor numérico entero, aunque la etiqueta de predicción es categórica, ¿cómo lo configuro para una característica categórica (que no sea un entero)? ¿Se requiere una conversión manual? 

Los datos de entrenamiento podrían tener etiquetas de clase como por ejemplo “Préstamo denegado”, “Préstamo otorgado”. El valor de predicción
devuelto por el punto final de puntuación de {{site.data.keyword.pm_full}} tiene valores como por ejemplo “0.0”, “1.0", etc. El punto final de puntuación también tiene una columna
opcional que contiene la representación de texto de predicción. Por ejemplo, si prediction=1.0, la columna predictionLabel podría tener un valor “Préstamo otorgado”. Si dicha columna está disponible, al configurar el resultado favorable y desfavorable para el modelo puede especificar los valores de serie “Préstamo otorgado” y “Préstamo denegado”. Si dicha columna no está disponible, debe especificar los valores de tipo entero/doble de 1.0, 0.0 para la clase favorable/desfavorable.

{{site.data.keyword.pm_full}} tiene un concepto de esquema de salida que define el esquema de la salida del punto final de puntuación de {{site.data.keyword.pm_full}} y el rol de las distintas
columnas. Los roles se utilizan para identificar qué columna contiene el valor de predicción, qué columna contiene la probabilidad de predicción, el valor de etiqueta de clase, etc. El esquema de salida se establece automáticamente para modelos creados utilizando el creador de modelos. También se puede establecer utilizando el cliente Python de {{site.data.keyword.pm_full}}. Los usuarios pueden utilizar el esquema de salida para definir una columna que contenga la representación de serie de la predicción. Para ello, se establece el valor de modeling_role para la columna en ‘decoded-target’. La documentación para el cliente Python de {{site.data.keyword.pm_full}} está disponible en: http://wml-api-pyclient-dev.mybluemix.net/#repository. Busque “OUTPUT_DATA_SCHEMA” para comprender el esquema de salida. La API que se utilizará es la API store_model que acepta OUTPUT_DATA_SCHEMA como parámetro.

### ¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?
{: #trainingdata}

Debe proporcionar {{site.data.keyword.aios_short}} acceso a los datos de entrenamiento almacenados en Db2 o {{site.data.keyword.cos_full_notm}}, o bien debe ejecutar un cuaderno que pueda acceder a los datos de entrenamiento. {{site.data.keyword.aios_short}} necesita acceder a sus datos de entrenamiento por las razones siguientes:

- Para generar explicaciones contrastativas: para crear explicaciones y acceder a estadísticas, como por ejemplo el valor medio, la desviación estándar y los valores individuales de los datos de entrenamiento necesarios.
- Para visualizar estadísticas de datos de entrenamiento: para llenar la página de detalles de sesgo, {{site.data.keyword.aios_short}} debe tener datos de entrenamiento a partir de los que generar las estadísticas.

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

En el enfoque basado en cuaderno, se espera que cargue las estadísticas y otra información al configurar un despliegue en {{site.data.keyword.aios_short}}. Esto implica que {{site.data.keyword.aios_short}} ya no tiene acceso a los datos de entrenamiento fuera del cuaderno, que se ejecuta en su entorno. Solo tiene acceso a la información cargada durante la configuración.


