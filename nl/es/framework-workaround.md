---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Integración de motores ML de terceros con {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} se integra con motores de servicio de aprendizaje automático externos, como Microsoft Azure ML Studio y Amazon
SageMaker.
{: shortdesc}

Puede integrar {{site.data.keyword.aios_short}} con motores de terceros de las maneras siguientes:

- Nivel de enlace de motor: posibilidad de listar despliegues y obtener detalles de los despliegues.
  
- Nivel de suscripción de despliegue: {{site.data.keyword.aios_short}} debe poder puntuar el despliegue de suscripción en el formato necesario, como el formato {{site.data.keyword.pm_full}} y recibir la salida en el mismo formato compatible. {{site.data.keyword.aios_short}} se debe configurar para
procesar formatos de entrada y salida.
   

- Registro de carga útil: cada entrada y salida al modelo desplegado activado por una aplicación de usuario se debe almacenar en un almacén de carga útil. El formato de los
registros de carga útil sigue la misma especificación que se menciona en la sección anterior sobre los niveles de suscripción de despliegue.
   
   {{site.data.keyword.aios_short}} utiliza estos registros para calcular el sesgo, y explicaciones, entre otras cosas más. No es posible que
{{site.data.keyword.aios_short}} almacene automáticamente las transacciones que se ejecutan en el sitio de usuario, que está fuera del sistema {{site.data.keyword.aios_short}}. Esta
es una de las formas en las que {{site.data.keyword.aios_short}} protege información propietaria. Utilice la API de REST o el SDK de Phyton de
{{site.data.keyword.aios_short}} para trabajar con datos seguros.
   
## Pasos para implementar esta solución
{: #fmrk-workaround-steps}

1. [Obtenga información sobre los motores de aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine).
2. [Configure el registro de carga útil](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload).
3. [Automatice el registro de carga útil](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg).
4. Configure un motor de aprendizaje automático personalizado mediante uno de estos [Ejemplos de motor aprendizaje automático personalizado](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).

