---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Creador de gráficos ![etiqueta beta](images/beta.png)
{: #chart_builder}

Utilice el creador de gráficos de {{site.data.keyword.aios_short}} para crear visualizaciones personalizadas, a fin de comprender mejor las predicciones y las entradas de los modelos en tiempo de ejecución. El creador de gráficos proporciona la posibilidad de ver la salida de la predicción del modelo en relación con las características o los rangos de datos que una empresa considera importantes. Ayuda a descubrir nuevas tendencias en los datos que pueden llevar a los equipos de ciencia empresarial y de datos a considerar realizar cambios en el modelo de inteligencia artificial. 
{: shortdesc}

Por ejemplo, si está familiarizado con nuestro modelo de riesgo crediticio de las guías de aprendizaje, puede ver la división en las clases previstas para los diferentes rangos del atributo Historial de crédito. 

   ![Un gráfico que muestra la predicción de la característica de sexo por la característica edad](images/by_custom_chart.png)
      
   También puede ver el grado de seguridad del modelo al realizar predicciones para estos rangos de Historial de crédito. Puede analizar la carga útil de puntuación que se envía al despliegue en el rango de datos seleccionado por gráfico personalizado (seleccionando características, clases de predicción y confianza).

   ![Un gráfico que muestra la predicción de la característica de sexo por la característica edad](images/by_custom_chart002.png)
   
