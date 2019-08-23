---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Descripción general de las métricas de equidad
{: #anlz_metrics_fairness}

Utilice la supervisión de equidad de {{site.data.keyword.aios_full}} para determinar si los resultados que genera el modelo son justos o no para el grupo supervisado. Cuando la supervisión de equidad está habilitada, de forma predeterminada genera un conjunto de métricas cada hora. Puede generar estas métricas bajo demanda pulsando el botón **Comprobar calidad ahora** o utilizando el cliente Python.
{: shortdesc}

{{site.data.keyword.aios_short}} identifica automáticamente si algún atributo protegido conocido está presente en un modelo. Cuando {{site.data.keyword.aios_short}} detecta estos atributos, automáticamente recomienda configurar los supervisores de sesgo para cada atributo presente, a fin de garantizar que se realiza el seguimiento en producción del sesgo en estos atributos potencialmente sensibles. 

Actualmente, {{site.data.keyword.aios_short}} detecta y recomienda supervisores para los siguientes atributos protegidos: 

- sexo
- grupo étnico
- estado civil
- edad
- código postal

Además de detectar los atributos protegidos, {{site.data.keyword.aios_short}} recomienda qué valores de cada atributo se deberían establecer como valores supervisados y cuáles como valores de referencia. Así, por ejemplo, {{site.data.keyword.aios_short}} recomienda que, para el atributo "Sexo", en el supervisor de sesgo se configure "Mujer" y "No binario" como valores supervisados y "Hombre" como valor de referencia. Si desea cambiar alguna de las recomendaciones, puede editarlas mediante el panel de configuración de sesgo. 

Los supervisores de sesgo recomendados ayudan a agilizar la configuración y garantizan que compruebe la equidad respecto a los atributos sensibles de sus modelos de inteligencia artificial. A medida que los reguladores prestan cada vez más atención al sesgo algorítmico, es cada vez más importante que las organizaciones comprendan el funcionamiento de sus modelos y si estos generan resultados injustos para determinados grupos.

## Información sobre la equidad
{: #mf-understand}

{{site.data.keyword.aios_short}} comprueba si su modelo desplegado está sesgado en tiempo de ejecución. Para detectar sesgos en un modelo desplegado,
debe definir atributos de equidad, como Edad o Sexo, tal como se detalla en la sección [Configuración del supervisor de
equidad](#mf-config) más abajo.

Es obligatorio especificar el esquema de salida para un modelo o función en {{site.data.keyword.pm_short}}, a fin de que la comprobación de sesgo esté habilitada en {{site.data.keyword.aios_short}}. El esquema de salida se puede especificar utilizando la propiedad `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` en la parte de metadatos de la API `store_model`. Para
obtener más información, consulte la [documentación
del cliente de {{site.data.keyword.pm_full}}](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### Cómo funciona
{: #mf-works}

Antes de configurar el supervisor de equidad debe comprender algunos conceptos clave imprescindibles:

- Los atributos de equidad son los atributos del modelo para los que este es probable que muestre un sesgo. Como ejemplo, para el atributo de equidad **`Sexo`**, el modelo podría estar sesgado para valores de sexo específicos (`Mujer`, `Transexual`, etc.) Otro ejemplo de atributo de equidad es **`Edad`**, donde el modelo podría estar sesgado para las personas de un grupo de edad, por ejemplo `de 18 a 25`.

- Valores de referencia y supervisados: los valores de los atributos de equidad se dividen en dos categorías distintas, Referencia y Supervisados. Los valores supervisados son aquellos para los que es probable que haya una discriminación. En el caso de un atributo de equidad como **`Sexo`**, los valores supervisados podrían ser `Mujer` y `Transexual`. Para un atributo de equidad numérico, por ejemplo **`Edad`**, los valores supervisados podrían ser `[18-25]`. Todos los demás valores de un atributo de equidad determinado se considerarán valores de referencia, por ejemplo `Sexo=Hombre` o `Edad=[26,100]`.

- Resultados favorables y desfavorables: la salida del modelo se categoriza como Favorable o Desfavorable. Como ejemplo, si el modelo predice si una persona debe obtener o no un préstamo, la columna Favorable podría ser `Préstamo otorgado` o `Préstamo otorgado parcialmente`, mientras que el resultado Desfavorable podría ser `Préstamo denegado`. Por lo tanto, el resultado Favorable es uno que se considera positivo, mientras que el resultado Desfavorable se considera negativo.

El algoritmo de {{site.data.keyword.aios_short}} calcula el sesgo cada hora, utilizando los últimos `N` registros presentes en la tabla de registro de carga útil; el valor de `N` se especifica al configurar la equidad. El algoritmo perturba estos últimos `N` registros para generar datos adicionales.

La perturbación se realiza cambiando el valor del atributo de equidad de Referencia a Supervisado, o viceversa. A continuación, los datos perturbados se envían al modelo para evaluar su comportamiento. El algoritmo considera los últimos `N` registros de la tabla de carga útil, y el comportamiento del modelo en los datos perturbados, para decidir si el modelo actúa de manera sesgada.

Se considera que un modelo está sesgado si, en este conjunto de datos combinado, el porcentaje de resultados favorables de la clase supervisada es inferior al porcentaje de resultados favorables para la clase de referencia, por algún valor de umbral. Este valor de umbral se especificará al configurar la equidad.

Los valores de equidad pueden ser superiores al 100%. Esto significa que el grupo supervisado ha recibido más resultados favorables que el grupo de referencia. Además, si no se envía ninguna solicitud de puntuación nueva, el valor de equidad se mantendrá constante.
{: note}

### Cómo calcularlo
{: #mf-bias-math}

La métrica de equidad utilizada en {{site.data.keyword.aios_short}} tiene un impacto desigual, y es una medida del índice con el que un grupo sin privilegios recibe un resultado determinado en comparación con el índice con el que el grupo con privilegios recibe el mismo resultado.

Se utiliza la fórmula matemática siguiente para calcular el impacto desigual:

```
                     (núm_positivos(privileged=False) / núm_instancias(privileged=False))
Impacto desigual =   ______________________________________________________________________

                     (núm_positivos(privileged=True) / núm_instancias(privileged=True))
```

donde `núm_positivos` es el número de personas del grupo (privileged=False, es decir, sin privilegios, o privileged=True, es decir, con privilegios) que han recibido un resultado positivo, y núm_instancias es el número total de personas del grupo.

El número resultante será un porcentaje, es decir, el porcentaje del índice con el que el grupo sin privilegios recibe el resultado positivo respecto al índice con el que lo recibe el grupo con privilegios. Por ejemplo, si un modelo de riesgo crediticio asigna la predicción “sin riesgo” al 80% de los solicitantes sin privilegios y al 100% de los solicitantes con privilegios, dicho modelo tendría un impacto desigual (que se presenta como la puntuación de equidad en {{site.data.keyword.aios_short}}) del 80%.

En {{site.data.keyword.aios_short}}, los resultados positivos se indican como los resultados favorables, y los resultados negativos se indican como los resultados desfavorables. El grupo con privilegios se designa como el grupo de referencia, y el grupo sin privilegios se designa como el grupo supervisado.


### Visualización del sesgo ![etiqueta beta](images/beta.png)
{: #mf-monitor-bias-viz}

Cuando se detecta un sesgo potencial, {{site.data.keyword.aios_short}} realiza varias funciones para confirmar si el sesgo es real. {{site.data.keyword.aios_short}} altera los datos invirtiendo el valor supervisado y el valor de referencia y luego ejecutando este nuevo registro con el modelo. A continuación, muestra la salida resultante como salida sin sesgo. {{site.data.keyword.aios_short}} también entrena un modelo sin sesgo duplicado que a continuación utiliza para detectar cuándo un modelo realizará una predicción sesgada. 

Se utilizan dos conjuntos de datos distintos para calcular la equidad y la exactitud. La equidad se calcula utilizando los datos de carga útil + alterados. La exactitud se calcula utilizando los datos de opinión. Para calcular la exactitud, {{site.data.keyword.aios_short}} necesita datos etiquetados manualmente, que sólo están presentes en la tabla de opinión.

Los resultados de estas determinaciones están disponibles en la visualización de sesgos, que incluye las vistas siguientes. Sólo puede ver las vistas si hay datos a los que dar soporte.

- **Carga útil + Alterados**: incluye la solicitud de puntuación recibida para la hora seleccionada más registros adicionales de las horas anteriores si no se cumple el número mínimo de registros necesarios para la evaluación. Incluye registros alterados/sintetizados adicionales utilizados para probar la respuesta del modelo cuando el valor de la característica supervisada cambia.

   Tome nota de los siguientes detalles de carga útil y alterados:

   - Número de registros que se leen durante esta hora de la tabla de carga útil
   - Registros adicionales que se leen de las horas anteriores (por ejemplo, si el valor `min_records` en la configuración de equidad se establece en 1000, y entre las 2 pm y las 3 pm solo se añaden 10 registros, para cumplir el requisito mínimo el sistema leería 990 registros adicionales de las horas anteriores).
   - Registros alterados por atributo de equidad
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo

  ![Ejemplo de carga útil más alterados](images/payload&perturbed.png)



- **Carga útil**: las solicitudes de puntuación reales recibidas por el modelo durante la hora seleccionada.

   Tome nota de los siguientes detalles de carga útil:
   
   - Número de registros que se leen o en los que se realiza la operación sin sesgo desde la tabla de carga útil
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo


  ![Ejemplo de datos de carga útil](images/payload.png)

- **Entrenamiento**: los registros de datos de entrenamiento utilizados para entrenar el modelo.

   Tome nota de los siguientes detalles de entrenamiento:
   
   - Número de registros de datos de entrenamiento. Los datos de entrenamiento se leen una vez, y la distribución se almacena en la variable `subscription/fairness_configuration`. Al calcular la distribución, deberíamos encontrar también el número de registros de datos de entrenamiento y almacenarlo en la misma distribución. Además, cuando se cambian los datos de formación, lo que indica que se ejecuta de nuevo el mandato `POST /data_distribution`, este valor se actualiza en la variable `fairness_configuration/training_data_distribution`. Al enviar la métrica, también deberíamos enviar este valor.
   - La hora a la que se procesan por última vez los datos de entrenamiento (primera vez y actualizaciones subsiguientes)

  ![Ejemplo de datos de entrenamiento](images/training.png)
   

   
- **Sin sesgo**: la salida del algoritmo sin sesgo tras procesar el tiempo de ejecución y los datos alterados. Al seleccionar el botón de selección **Sin sesgo** se muestran los cambios en el modelo sin sesgo, en comparación con el modelo en producción. El gráfico refleja el estado de resultados mejorados para los grupos.


   Tome nota de los siguientes detalles sin sesgo:
   
   - Número de registros que se leen/en los que se realiza la operación sin sesgo desde la tabla de carga útil
   - Registros adicionales que se leen para realizar sesgo, y por lo tanto también sin sesgo. El mismo número que en la selección `Carga útil + Alterados`
   - Registros alterados por atributo de equidad
   - Indicación de fecha y hora del registro de mayor antigüedad del periodo de tiempo para el que se debe calcular el sesgo
   - Indicación de fecha y hora del registro más nuevo o último del periodo de tiempo para el que se debe calcular el sesgo
   - Se muestran valores de equidad anteriores y posteriores en la parte de cabecera de la vista Con sesgo. 
      - La exactitud **posterior** se calcula tomando los datos de opinión y enviándolos a la API de eliminación activa del sesgo. Esta API devuelve la predicción sin sesgo. Los datos de opinión también contienen la etiqueta manual. La etiqueta manual se compara con la predicción sin sesgo para calcular la exactitud. Esta API devuelve la predicción sin sesgo. La tabla de opinión también contiene la etiqueta manual. La etiqueta manual se compara con la predicción sin sesgo para calcular la exactitud. 
      - La exactitud **anterior** se calcula utilizando los mismos datos de opinión. Para el cálculo de la exactitud anterior, los datos de opinión se envían al modelo para obtener su predicción y el valor previsto se compara con la etiqueta manual para obtener la exactitud.

  ![Ejemplo de datos sin sesgo](images/debiased.png)
  
### Ejemplo
{: #mf-ex1}

Considere un punto de datos donde, para `Sexo=Hombre` (Valor de referencia), el modelo predice un resultado favorable, pero cuando se perturba el registro cambiando `Sexo` a `Mujer` (valor supervisado), mientras se mantienen sin cambios todos los demás valores de características, el modelo predice un resultado desfavorable. En general se dice que un modelo muestra sesgo si hay puntos de datos suficientes (en los últimos `N` registros de la tabla de carga útil, más los datos perturbados) donde el modelo actúa de manera sesgada.

### Modelos soportados
{: #mf-supmo}

 {{site.data.keyword.aios_short}} da soporte a la detección de sesgo sólo para aquellos modelos y funciones Python que esperan alguna clase de datos estructurados en su vector de característica.

Las métricas de equidad se calculan en función de la siguiente información:

- Los datos de carga útil de puntuación.

Para una supervisión adecuada, cada solicitud de puntuación se debe registrar también en {{site.data.keyword.aios_short}}. El registro de datos de carga útil está automatizado para los motores de {{site.data.keyword.pm_full}}.

Para otros motores de aprendizaje automático, los datos de carga útil se pueden proporcionar mediante el cliente Python o la API REST.

Para motores de aprendizaje automático que no sean {{site.data.keyword.pm_full}}, la supervisión de equidad crea solicitudes de puntuación adicionales en el despliegue supervisado.
{: note}

Puede revisar los valores de todas las métricas a lo largo del tiempo en el panel de control de {{site.data.keyword.aios_short}}:

![gráfico de métricas de equidad que muestra una desviación por debajo del umbral](images/fairness_metrics_001.png)

Puede revisar los detalles relacionados, como los resultados favorables y desfavorables:

![Detalles de equidad](images/fairness_metrics_002.png)

Puede ver las transacciones detalladas:

![Un gráfico sobre equidad que muestra una lista de transacciones](images/fairness_metrics_003.png)

Puede ver el punto final de puntuación sesgada recomendado:

![Detalles del punto final de puntuación sesgada](images/fairness_metrics_004.png)

### Métricas de equidad recomendadas
{: #anlz_metrics_supfairmets}

{{site.data.keyword.aios_short}} da soporte a las métricas de equidad siguientes:

- [Equidad para un grupo](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

{{site.data.keyword.aios_short}} da soporte a los siguientes atributos protegidos: 

- [sexo](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [grupo étnico](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [estado civil](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [edad](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [código postal](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### Detalles de equidad soportados
{: #anlz_metrics_supfairdets}

{{site.data.keyword.aios_short}} da soporte a los siguientes detalles de métricas de equidad:

- Los porcentajes favorables para cada uno de los grupos
- Los promedios de equidad para todos los grupos de equidad

```
                          (% de resultados favorables en grupo supervisado
Índice de impacto desigual =  ____________________________________________
                              (% de resultados favorables en grupo de referencia)
```

- Distribución de los datos para cada uno de los grupos supervisados
- Distribución de los datos de carga útil
