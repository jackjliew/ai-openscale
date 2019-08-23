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

# Configuración del supervisor de equidad
{: #mf-monitor}

En {{site.data.keyword.aios_full}}, el supervisor de equidad explora si existe sesgo en el despliegue, a fin de garantizar resultados justos para las distintas poblaciones.
{: shortdesc}

## Pasos
{: #mf-config}

En la pestaña **Equidad**, en la página **¿Qué es la equidad?**, pulse **Iniciar** para iniciar el proceso de configuración.

![Página ¿Qué es la equidad?](images/fair-what-is.png)

Durante todo este proceso, {{site.data.keyword.aios_full}} analiza el modelo y realiza las recomendaciones según el resultado más lógico. En las páginas sucesivas de la pestaña **Equidad** debe realizar las tareas siguientes:

1. Seleccione las características que desea supervisar. Sólo se da soporte a las características de un tipo de datos de equidad categórico, numérico (entero), flotante o doble. No se da soporte a características con otros tipos de datos.

1. Especifique grupos de referencia y supervisados.

   Cada característica tiene requisitos específicos para configurar. Por ejemplo, si elige `edad` como una de las características supervisadas, debe definir los rangos de edad para un **Grupo de referencia** y un **Grupo supervisado** especificando los valores directamente en cada grupo.

1.  Establezca el umbral de alerta de equidad para la característica.

    Se utiliza un umbral de equidad para especificar una diferencia aceptable entre el porcentaje de resultados favorables para el grupo supervisado en comparación con el porcentaje de resultados favorables para el grupo de referencia.

    Considere un modelo que predice quién debe obtener un préstamo (`resultado favorable=préstamo otorgado`) y quién no (`resultado desfavorable=préstamo denegado`). Además, el valor supervisado de edad es `[18,25]` y el valor de referencia es `[26,100]`. Cuando se ejecuta el algoritmo de detección de sesgo, este encuentra que el porcentaje de resultados favorables para las personas del grupo de edad `[18,25]` en los últimos `N` registros más los datos perturbados es del `50%`, mientras que el porcentaje de resultados favorables para las personas del grupo de edad `[26,100]` es del `70%`, la equidad se calcula como 50*100/70 = 71,42.

    Si el umbral de equidad está establecido en el 80%, el algoritmo marcará el modelo como sesgado, ya que la equidad que se ha calculado supera
el umbral. Sin embargo, si el umbral se establece en el 70%, no notificará el modelo como sesgado.

     Los valores que especifique en estas pantallas deben ser los que se envían al punto final de puntuación del modelo (y, en consecuencia, se añadirán a la tabla de carga útil). Si los datos se manipulan antes de enviarlos al punto final de puntuación, especifique los valores manipulados. Por ejemplo, si los datos originales tenían valores de `Hombre` y `Mujer` para *Sexo* y se han manipulado de forma que los datos enviados al punto final de puntuación han sido `H` y `M`, especifique `H` y `M` en la pantalla.

1.  Especifique valores que representen un resultado favorable para el modelo. Los valores se derivan de la columna `etiqueta` de los [datos de entrenamiento](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), si el esquema de salida del modelo contiene una columna de correlación. En
{{site.data.keyword.pm_full}}, la columna `predicción` siempre tiene un valor doble. La columna de correlación se utiliza para especificar la correlación de este valor `predicción` en la etiqueta de clase.

    Por ejemplo, si el valor `predicción` es `1.0`, la columna de correlación podría tener un valor de `Préstamo denegado`; esto implica que la predicción del modelo es `Préstamo denegado`. Por lo tanto, si el esquema de salida del modelo contiene una columna de correlación, especifique los valores Favorable y Desfavorable utilizando aquellos presentes en la columna de correlación.

    Sin embargo, si la columna de correlación no está presente en el esquema de salida del modelo, los valores Favorable y Desfavorable se deben especificar utilizando el valor de la columna `predicción` (`0.0`, `1.0`, etc.)

1.  Finalmente, establezca un tamaño de muestra mínimo, para evitar la medición de equidad hasta que haya disponible un número mínimo de registros en el conjunto de datos de evaluación. Esto garantiza que el tamaño de la muestra no es demasiado pequeño y pueda causar desviaciones en los resultados. Cada vez que se ejecuta la comprobación de sesgo, se utilizará el tamaño mínimo de muestra para decidir el número de registros sobre el que se calculará el sesgo.

    Aparece un resumen de sus selecciones para su revisión. Si desea cambiar algo, pulse el enlace **Editar** para esa sección; de lo contrario, pulse **Guardar**.

    También puede pulsar **Añadir otra característica** para volver a la pantalla de selección de características y añadir más características, por ejemplo `Ciudad`, `Código postal` o `Saldo de cuenta` al Supervisor de equidad.

### Cómo funciona la eliminación del sesgo
{: #mf-debias}

Para comprobar el punto final sin sesgo, pulse el botón **Eliminar sesgo de punto final**. Podrá ver y copiar el punto final en distintos formatos, como cURL, Java o Python. 

El punto final de puntuación sin sesgo se puede utilizar exactamente como el punto final de puntuación normal del modelo desplegado. Además de devolver la respuesta del modelo desplegado, también devuelve dos columnas `debiased_prediction` y `debiased_probability`.

- La columna `debiased_prediction` contiene el valor de predicción sin sesgo. En el caso de {{site.data.keyword.pm_full}},
es la representación codificada de la predicción. Por ejemplo, si la predicción del modelo es "Préstamo otorgado" o "Préstamo denegado", {{site.data.keyword.pm_full}} puede codificar estos dos valores como "0.0" y "1.0", respectivamente. La columna `debiased_prediction` contiene dicha representación codificada de la predicción sin sesgo.

- La columna `debiased_probability`, por otro lado, representa la probabilidad de la predicción sin sesgo. Se trata de una matriz de valor doble, donde cada valor representa la probabilidad de la predicción sin sesgo perteneciente a una de las clases de predicción.

También se devuelve otra columna, `debiased_decoded_target`, en caso de que tenga una columna en el esquema de salida que contenga una columna con `modeling-role` como `decoded-target`.

- La columna `debiased_decoded_target` contiene la representación de serie de la predicción sin sesgo. En el ejemplo anterior,
donde el valor de predicción era "0.0" o "1.0", `debiased_decoded_target` contendrá "Préstamo otorgado" o "Préstamo denegado".

Idealmente, llamaría directamente a este punto final desde su aplicación de producción, en lugar de llamar directamente al punto final de puntuación de su modelo desplegado en el motor de servicio del modelo ({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, etc.) De esta forma, {{site.data.keyword.aios_short}} también almacenará los valores `sin sesgo` en la tabla de registro de carga útil de su modelo de despliegue. A continuación, se eliminará automáticamente el sesgo de toda la puntuación realizada mediante este punto final.

Puesto que este punto final se ocupa del sesgo en tiempo de ejecución, continuará realizando comprobación en segundo plano de los últimos datos de puntuación de la tabla de registro de carga útil, y continuará actualizando el modelo de mitigación de sesgos que se utiliza para eliminar el sesgo de las solicitudes de puntuación. De esta forma, {{site.data.keyword.aios_short}} está siempre actualizado con los últimos datos entrantes, y con su comportamiento para detectar y mitigar sesgos.

Finalmente, {{site.data.keyword.aios_short}} utiliza un umbral para decidir qué datos son ahora aceptables y se consideran ahora sin sesgo. Este umbral se toma como el valor mínimo de los umbrales establecidos en el supervisor de equidad para todos los atributos de equidad configurados.

## Pasos siguientes
{: #mf-next}

Para continuar configurando supervisores, pulse la pestaña **Desviación** y pulse **Empezar**. Para obtener más información, consulte [Configuración del supervisor de detección de desviación](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
