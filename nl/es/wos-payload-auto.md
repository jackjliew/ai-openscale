---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Automatización del registro de carga útil
{: #fmrk-workaround-pyld-lg}

Existe registro de carga útil automático entre {{site.data.keyword.aios_full}} y {{site.data.keyword.pm_full}} cuando estos se suministran en la misma cuenta de {{site.data.keyword.Bluemix_notm}}. También puede automatizar el registro de carga útil para otros proveedores de aprendizaje automático, o para una instancia de {{site.data.keyword.pm_full}} que no esté en la misma cuenta, utilizando uno de los siguientes casos y opciones:
{: shortdesc}

### Caso 1: Mantenga el formato original de entrada y salida de puntuación (diferente del que precisa {{site.data.keyword.aios_short}})
{: #fmrk-workaround-case1}

Si las aplicaciones utilizan un formato de carga útil original que no se puede cambiar, elija una de las opciones siguientes:

- Opción 1: el punto final de puntuación del motor de aprendizaje automático personalizado debe aceptar los dos formatos de carga útil. 

   En función del formato de la carga útil: {{site.data.keyword.aios_short}} (parecido a {{site.data.keyword.pm_full}}) o el del
usuario
devuelve la salida en el formato correspondiente. Si el formato es el del usuario conviértalo a uno de {{site.data.keyword.aios_short}}
y almacénelo como registro de carga útil en la tabla de registro de carga útil. Si el formato de entrada de puntuación es uno de {{site.data.keyword.aios_short}}, no almacene la carga útil (esta carga útil proviene
de {{site.data.keyword.aios_short}} no del usuario).

   Para obtener más información, consulte
[Utilización de
dos formatos de carga útil](#fmrk-workaround-notsuppt).

- Opción 2: Si por algunos motivos no es posible incluir esta lógica en un único punto final de API REST, puede definir dos puntos finales. 

   Uno lo utiliza la aplicación; no obstante, debe añadir registro de carga útil y convertirlo al formato previsto. El segundo punto final lo utiliza
{{site.data.keyword.aios_short}} para realizar cálculos necesarios, por ejemplo, sesgo y explicabilidad. No se requiere ningún registro de carga
útil para este punto final. Durante la configuración de {{site.data.keyword.aios_short}}, el segundo punto final debe apuntar a uno con formatos compatibles.

   Para obtener más información, consulte
[Utilización de
dos puntos finales](#fmrk-workaround-opt2-cs1).

- Opción 3: Mover el módulo de registro de carga útil al punto final original o a la aplicación en sentido descendente. 

   Si la aplicación da soporte a esta opción, sólo es necesario desarrollar un punto final en el motor de aprendizaje automático personalizado: el de
{{site.data.keyword.aios_short}}.

### Case 2: Trabaje con el formato de carga útil que requiera {{site.data.keyword.aios_short}}
{: #fmrk-workaround-case2}

En tal caso, no hay necesidad de efectuar ninguna conversión del formato del usuario (entrada/salida de puntuación) al que precisa
{{site.data.keyword.aios_short}}.

Debido a que no deseamos tener las solicitudes de puntuación internas registradas como carga útil de usuario
(cálculos realizados por {{site.data.keyword.aios_short}}),
debe desarrollar dos puntos finales o debe codificar lógica adicional para un único punto final.

- Opción 1: dos puntos finales. Es casi lo mismo que la opción 2 en el caso 1. La única diferencia es que no hay ninguna necesidad de hacer
conversiones de formato ya que éstas ya están alineadas.

- Opción 2: Único punto final. Es necesario detectar si la solicitud de puntuación proviene de la aplicación del usuario. Esto se puede lograr
mediante el envío de información adicional en la puntuación de la carga útil (también conocida como metadatos). Si dichos metadatos se detectan, se debe
registrar la carga útil.

## Utilización de dos formatos de carga útil
{: #fmrk-workaround-notsuppt}

Supongamos que utilizo la oferta XYZ para servir a mis modelos. {{site.data.keyword.aios_short}} no da soporte a XYZ en esta etapa.

Tengo muchas aplicaciones en sentido descendente que consumen mis despliegues en XYZ y no puedo cambiar el formato de la carga útil de puntuación. No
obstante, puedo modificar la lógica de punto final de puntuación.

### Pasos

1. Desarrollar un motor de máquina de aprendizaje automático que englobe el despliegue de XYZ.
2. Implementar el punto final de puntuación en el motor de aprendizaje automático para dar soporte a los formatos de carga útil para XYZ y
{{site.data.keyword.aios_short}}.
3. Añadir la lógica en el punto final de puntuación en el motor de aprendizaje automático personalizado para detectar el formato de la carga útil.
4. Si la carga útil proviene de aplicaciones descendientes, conviértala al formato de {{site.data.keyword.aios_short}} y regístrela como
registros de carga útil en
{{site.data.keyword.aios_short}}.
5. Conmute los puntos finales de puntuación de las aplicaciones en sentido descendente a la nueva que ha creado.

Si el URL del punto final de puntuación debe seguir siendo el mismo, utilice la redirección de URL, que también se conoce como proxy.

## Utilización de dos puntos finales
{: #fmrk-workaround-opt2-cs1}

Si el formato de la carga útil no se puede cambiar, por ejemplo, si hace que las aplicaciones en sentido descendente se interrumpan, debe utilizar
puntos
finales independientes. Este enfoque consta de los componentes siguientes:

- punto final de puntuación (en el formato del usuario) con el punto final de puntuación original utilizando el formato definido por el usuario para la entrada y para la salida
- motor ml personalizado con punto final de perturbación (formato {{site.data.keyword.aios_short}}) y punto final de descubrimiento. El
punto final de la turbación incluye el punto final de puntuación original más hace conversiones del formato de {{site.data.keyword.aios_short}} a
uno del
usuario y de la salida del usuario a uno de {{site.data.keyword.aios_short}}. Esto es necesario para que {{site.data.keyword.aios_short}}
realice una solicitud de puntuación correcta y entienda la salida.
- derivador de punto final de puntuación con prestación de registro de carga útil. Este derivador lo consume la aplicación en sentido descendente en
lugar del punto final de puntuación. Su lógica se ha ampliado con la posibilidad de registro de carga útil. Cada vez que la solicitud de puntuación se ejecuta se convierten la entrada y la
salida al formato de
{{site.data.keyword.aios_short}} y se registra.

El siguiente diagrama de flujo muestra la solución de motor de aprendizaje automático personalizado en la que el motor de aprendizaje automático
personalizado maneja los puntos finales de perturbación y descubrimiento y los convierte al formato:

![Especificación de puntos finales de API REST](images/woscustommlworkflow.png)

### Pasos
{: #fmrk-workaround-smple-cd}

1. Utilice un cuaderno para crear un punto final de puntuación para el  despliegue del modelo de riesgo crediticio (scikit-learn) en Microsoft Azure Machine Learning Service. Para obtener más información, consulte
[este
cuaderno de ejemplo](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb).
2. Crear un motor de aprendizaje automático personalizado en Microsoft Azure Cloud como aplicación Flask. Cree los puntos finales de perturbación y
descubrimiento. Para obtener más información, consulte
[estas instrucciones de despliegue](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure).
3. Configure {{site.data.keyword.aios_short}} para que funcione con el motor de aprendizaje automático personalizado. Para obtener más
información, consulte
[este
cuaderno de ejemplo](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb).
4. Cree un derivador de punto final de puntuación que automatice Microsoft Azure Machine Learning Service. Para obtener más
información, consulte
[este
cuaderno de ejemplo](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb).

Preste especial atención a los elementos siguientes:

- Credenciales: Para facilitar el seguimiento de la guía de aprendizaje, las credenciales de {{site.data.keyword.aios_short}} están
grabadas en el código (derivador de punto final de puntuación). Debe actualizar estos valores en las credenciales reales.
- Python SDK frente a API REST: La guía de aprendizaje utiliza el SDK de Python para registrar la carga útil. Para ello, también puede utilizar la API
REST, pero debe generar o renovar la señal por su cuenta. 
- {{site.data.keyword.cloud_notm}}frente a Cloud Pak for Data: Si utiliza {{site.data.keyword.wos4d_notm}}, las credenciales están
en un formato diferente
[aquí
tiene el cuaderno de ejemplo](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb). La clase de cliente de {{site.data.keyword.aios_short}} también es distinta. Utiliza
la clase cliente `APIClient4ICP`.
- Registro de carga útil como paquete/punto final separado — extracción de métodos de registro de carga útil y conversión para
separar paquete o punto final. De este modo, se podría volver a utilizar si quisiera inyectar un lote de cargas útiles fuera del derivador de punto final.

