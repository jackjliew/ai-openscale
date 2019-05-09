---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# Preguntas más frecuentes
{: #wos-faqs}

Aquí encontrará algunas de las preguntas más frecuentes de los usuarios de {{site.data.keyword.aios_full}}.
{: shortdesc}

## Preguntas
{: #wos-faqs-questions}

- [¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?](#wos-faqs-convert-data-types)

### ¿Cómo convierto una columna de predicción de un tipo de datos entero a un tipo de datos categórico?
{: #wos-faqs-convert-data-types}

Al configurar la supervisión de la equidad para un modelo, la columna de predicción sólo permite un valor numérico entero, aunque la etiqueta de predicción es categórica, ¿cómo lo configuro para una característica categórica (que no sea un entero)? ¿Se requiere una conversión manual? 

Los datos de entrenamiento podrían tener etiquetas de clase como por ejemplo “Préstamo denegado”, “Préstamo otorgado”. El valor de predicción devuelto por el punto final de puntuación de WML tiene valores como por ejemplo “0.0”, “1.0", etc. El punto final de puntuación también tiene una columna opcional que contiene la representación de texto de predicción. Por ejemplo, si prediction=1.0, la columna predictionLabel podría tener un valor “Préstamo otorgado”. Si dicha columna está disponible, al configurar el resultado favorable y desfavorable para el modelo puede especificar los valores de serie “Préstamo otorgado” y “Préstamo denegado”. Si dicha columna no está disponible, debe especificar los valores de tipo entero/doble de 1.0, 0.0 para la clase favorable/desfavorable.

WML tiene un concepto de esquema de salida que define el esquema de la salida del punto final de puntuación de WML y el rol de las distintas columnas. Los roles se utilizan para identificar qué columna contiene el valor de predicción, qué columna contiene la probabilidad de predicción, el valor de etiqueta de clase, etc. El esquema de salida se establece automáticamente para modelos creados utilizando el creador de modelos. También se puede establecer utilizando el cliente Python de WML. Los usuarios pueden utilizar el esquema de salida para definir una columna que contenga la representación de serie de la predicción. Para ello, se establece el valor de modeling_role para la columna en ‘decoded-target’. La documentación del cliente Python de WML está disponible en: http://wml-api-pyclient-dev.mybluemix.net/#repository. Busque “OUTPUT_DATA_SCHEMA” para comprender el esquema de salida. La API que se utilizará es la API store_model que acepta OUTPUT_DATA_SCHEMA como parámetro.



