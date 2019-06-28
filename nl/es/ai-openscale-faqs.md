---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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
{:faq: data-hd-content-type='faq'}

# Preguntas más frecuentes
{: #wos-faqs}

Aquí encontrará algunas de las preguntas más frecuentes de los usuarios de {{site.data.keyword.aios_full}}.
{: shortdesc}

## Preguntas
{: #wos-faqs-questions}

- [¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?](#wos-faqs-convert-data-types)
- [¿Por qué {{site.data.keyword.aios_short}} necesita acceder a mis datos de entrenamiento?](#trainingdata)

### ¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?
{: #wos-faqs-convert-data-types}

Al configurar la supervisión de la equidad para un modelo, la columna de predicción sólo permite un valor numérico entero, aunque la etiqueta de predicción es categórica, ¿cómo lo configuro para una característica categórica (que no sea un entero)? ¿Se requiere una conversión manual? 

Los datos de entrenamiento podrían tener etiquetas de clase como por ejemplo “Préstamo denegado”, “Préstamo otorgado”. El valor de predicción devuelto por el punto final de puntuación de WML tiene valores como por ejemplo “0.0”, “1.0", etc. El punto final de puntuación también tiene una columna opcional que contiene la representación de texto de predicción. Por ejemplo, si prediction=1.0, la columna predictionLabel podría tener un valor “Préstamo otorgado”. Si dicha columna está disponible, al configurar el resultado favorable y desfavorable para el modelo puede especificar los valores de serie “Préstamo otorgado” y “Préstamo denegado”. Si dicha columna no está disponible, debe especificar los valores de tipo entero/doble de 1.0, 0.0 para la clase favorable/desfavorable.

WML tiene un concepto de esquema de salida que define el esquema de la salida del punto final de puntuación de WML y el rol de las distintas columnas. Los roles se utilizan para identificar qué columna contiene el valor de predicción, qué columna contiene la probabilidad de predicción, el valor de etiqueta de clase, etc. El esquema de salida se establece automáticamente para modelos creados utilizando el creador de modelos. También se puede establecer utilizando el cliente Python de WML. Los usuarios pueden utilizar el esquema de salida para definir una columna que contenga la representación de serie de la predicción. Para ello, se establece el valor de modeling_role para la columna en ‘decoded-target’. La documentación del cliente Python de WML está disponible en: http://wml-api-pyclient-dev.mybluemix.net/#repository. Busque “OUTPUT_DATA_SCHEMA” para comprender el esquema de salida. La API que se utilizará es la API store_model que acepta OUTPUT_DATA_SCHEMA como parámetro.

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


