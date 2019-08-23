---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Las explicaciones contrastivas utilizan positivos pertinentes y negativos pertinentes
{: #ie-pp-pn}

Para las explicaciones contrastivas, {{site.data.keyword.aios_short}} muestra valores de positivos pertinentes y de negativos pertinentes. 
{: shortdesc}

- Los positivos pertinentes son hallazgos que son críticos para determinar qué es algo.
- Los negativos pertinentes son hallazgos no encontrados que son importantes por su ausencia.

{{site.data.keyword.aios_short}} muestra siempre un positivo pertinente. Sin embargo, a veces no hay ningún negativo pertinente para mostrar. En este caso, los valores de esta característica ya están en el valor medio o la predicción no ha cambiado como resultado de alejar los valores del valor medio.

Para comprender esto mejor, considere que cuando {{site.data.keyword.aios_short}} calcula el valor negativo pertinente, cambia los valores de todas las características alejándolos de su valor medio. Para los negativos pertinentes, esto indica los valores de la característica que están más alejados del valor medio. Si los valores de un punto de datos ya están en el valor medio o si incluso tras cambiar el valor alejándolo del valor medio la predicción no cambia, no hay negativos pertinentes para mostrar. En caso de positivos pertinentes, {{site.data.keyword.aios_short}} encuentra el cambio máximo en los valores de la característica hacia el valor medio, de tal forma que la predicción no cambia. En la práctica, esto significa que casi siempre hay un positivo pertinente para explicar una transacción.

