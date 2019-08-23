---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# Equidad para un grupo
{: #quality_group}

La métrica Equidad para un grupo proporciona la propensión del modelo a entregar resultados favorables a un grupo más que a otro. Un grupo puede ser cualquier grupo, como edad, sexo o raza.
{: shortdesc}

## Detalles de Equidad para un grupo
{: #quality_group-glance}

- **Descripción**: la propensión de los modelos a entregar resultados favorables a un grupo más que a otro.
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**: punto final de puntuación sesgada que puede utilizar en su aplicación empresarial para recibir respuestas sesgadas del modelo desplegado.
- **Tipo de problema**: todos
- **Tipo de datos**: estructurados
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: sí

## Atributos protegidos
{: #quality_group-atts}

{{site.data.keyword.aios_short}} identifica automáticamente si algún atributo protegido conocido está presente en un modelo. Cuando {{site.data.keyword.aios_short}} detecta estos atributos, automáticamente recomienda configurar los supervisores de sesgo para cada atributo presente, a fin de garantizar que se realiza el seguimiento en producción del sesgo en estos atributos potencialmente sensibles. 

### sexo
{: #quality_group-sex}

{{site.data.keyword.aios_short}} recomienda que, para el atributo **Sexo**, en el supervisor de sesgo se configure `Mujer` y `No binario` como valores supervisados y `Hombre` como valor de referencia. 

### grupo étnico
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} recomienda que, para el atributo **grupo étnico**, en el supervisor de sesgo se configure `Blanco/caucásico` como valor de referencia y los otros grupos étnicos como valores supervisados.

### estado civil
{: #quality_group-marital}

{{site.data.keyword.aios_short}} recomienda que, para el atributo **estado civil**, en el supervisor de sesgo se configure `casado` como valor de referencia y `soltero` como valor supervisado.

### edad
{: #quality_group-age}

{{site.data.keyword.aios_short}} recomienda que, para el atributo **edad**, el supervisor de sesgo se configure de manera que el rango de edades lleve a la eliminación práctica del sesgo.

### código postal
{: #quality_group-zip}

{{site.data.keyword.aios_short}} recomienda que, para el atributo **código postal**, el supervisor de sesgo se configure de tal forma que se puntúen códigos postales individuales.

## Interpretación de la pantalla
{: #quality_group-display}

### Puntuación de equidad para un grupo
{: #quality_group-display-fairnessscore}



### Grupos supervisados
{: #quality_group-display-monitoredgroups}



### Planificación
{: #quality_group-display-schedule}

El panel **Planificación** muestra 



