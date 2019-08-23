---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Infraestructuras IBM SPSS C&DS
{: #frmwrks-spss}

Puede utilizar IBM SPSS C&DS para realizar el registro de carga útil y el registro de opiniones, y para medir la exactitud del rendimiento, la detección de sesgos en tiempo de ejecución, la explicabilidad y la función de eliminación automática de sesgo en {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} tiene planificado dar soporte completo a las siguientes infraestructuras de IBM SPSS Collaboration and Deployment Services (C&DS):
{: shortdesc}

Actualmente, el soporte se limita a {{site.data.keyword.wos4d_full}}.
{: note}

Tabla 1. Detalles del soporte de las infraestructuras

| Infraestructura | Tipo de problema | Tipo de datos |
|:---|:---:|:---:|
| SPSS | Clasificación | Estructura |
{: caption="Detalles del soporte de las infraestructuras" caption-side="top"}

Si el `ID de despliegue` para una suscripción contiene un carácter de subrayado, la exactitud con sesgo que aparece normalmente en la pestaña con sesgo de la métrica de equidad no se visualizará.
{: note}


## Soporte de explicabilidad para las infraestructuras de IBM SPSS Collaboration and Deployment Services (C&DS)
{: #frmwrks-spss-exp-supp}

- La explicabilidad está soportada para modelos binarios y para modelos multiclase SPSS que devuelven probabilidades para todas las clases. 
- La explicabilidad no está soportada para modelos multiclase SPSS que devuelven únicamente la probabilidad de clase ganadora.



