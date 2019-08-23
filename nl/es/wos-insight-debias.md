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

# Opciones para la eliminación del sesgo
{: #it-dbo}

{{site.data.keyword.aios_short}} utiliza dos tipos de eliminación del sesgo: pasiva y activa. La eliminación pasiva del sesgo le permite saber cómo se ha eliminado el sesgo, mientras que la eliminación activa del sesgo le impide continuar con el sesgo al cambiar el modelo en tiempo real para la aplicación actual.

- *Eliminación pasiva del sesgo*: la eliminación pasiva del sesgo es el trabajo que OpenScale realiza por su cuenta, automáticamente, cada hora. Se considera pasiva porque se lleva a cabo sin la interacción del usuario. Cuando {{site.data.keyword.aios_short}} comprueba si hay sesgo, también elimina el sesgo de los datos, analizando el comportamiento del modelo e identificando los datos donde el modelo actúa de forma sesgada.

  A continuación, {{site.data.keyword.aios_short}} crea un modelo de aprendizaje automático para predecir si es probable que el modelo actúe de forma sesgada en un nuevo punto de datos determinado. {{site.data.keyword.aios_short}} analiza los datos que recibe el modelo cada hora y busca los puntos de datos donde {{site.data.keyword.aios_short}} cree que el modelo actúa de forma sesgada. Para estos puntos de datos, el atributo de equidad se perturba de minoría a mayoría, y los datos perturbados se envían al modelo original para la predicción. Esta predicción del modelo original se utiliza como la salida sin sesgo.

  {{site.data.keyword.aios_short}} realiza esta eliminación de sesgo cada hora, en todos los datos que ha recibido el modelo durante la última hora. También calcula la equidad de la salida sin sesgo y la muestra en la pestaña **Modelo sin sesgo**.

- *Eliminación activa del sesgo*: la eliminación activa del sesgo es una manera de solicitar e incorporar los resultados sin sesgo a la aplicación mediante el punto final de API REST. Indica activamente a {{site.data.keyword.aios_short}} que ejecute la eliminación del sesgo y que modifique el modelo para que se pueda ejecutar la aplicación sin sesgo. En la eliminación activa del sesgo, puede utilizar un punto final de API REST de eliminación de sesgo desde su aplicación. Este punto final de API REST llamará inmediatamente a su modelo y comprobará su comportamiento.

  Si {{site.data.keyword.aios_short}} detecta que el modelo actúa de forma sesgada, perturba los datos mencionados anteriormente y los envía
de nuevo al modelo original. La salida del modelo original en los datos perturbados se devolverá como la predicción no sesgada. Si {{site.data.keyword.aios_short}} determina que el modelo original no actúa de forma sesgada, {{site.data.keyword.aios_short}} devolverá la predicción del modelo original como la predicción no sesgada. Por lo tanto, utilizando este punto final de API REST, puede asegurarse de que la aplicación no toma decisiones en función de la salida sesgada de los modelos.

Seleccione el enlace **Punto final de puntuación sin sesgo** para buscar el punto final de API REST sin sesgo

![Se muestra la pantalla de detalles Eliminar sesgo de punto final de API con el ejemplo de cURL que se muestra en el recuadro del fragmento de código](images/insight-debias-api.png)

## Pasos siguientes
{: #it-dbo-nextsteps}

- Para mitigar el sesgo, una vez detectado, debe crear una nueva versión del modelo que corrija el problema. {{site.data.keyword.aios_short}} almacena los registros sesgados en la tabla de etiquetado manual. Es necesario etiquetar manualmente estos registros sesgados y a continuación reentrenar el modelo utilizando estos datos adicionales para crear una nueva versión sin sesgo del modelo.


