---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: upgrading, configuration, configuring, deployment, subscription, service plans, plans

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

# Actualización de {{site.data.keyword.aios_short}} de un plan Lite a un plan de pago
{: #cf-upgrade}

Puede actualizar {{site.data.keyword.aios_full}} de un plan Lite gratuito a un plan de pago mediante el panel de control de {{site.data.keyword.Bluemix}}. ¿Cómo sabe que es el momento de actualizar? Si obtiene mensajes de error, como por ejemplo `403 Errors.AIQFM0011: 'El plan Lite ha excedido la limitación de 50.000 filas para Eliminar sesgo`.
{: shortdesc}

1. En el panel de control de {{site.data.keyword.aios_short}}, pulse el avatar.
2. Pulse **Ver opciones de actualización**.
4. Establezca el recuadro de selección **Estándar** y a continuación pulse **Actualizar**.

Tras la actualización, esta requiere unos 5 minutos para hacerse efectiva. Es posible que obtenga un mensaje de error durante este período, pero tras la actualización los mensajes de error sobre limitaciones excedidas desaparecerán.

## Pasos siguientes
{: #cf-upgrade-ns}

Para comprender mejor cómo actualizar los servicios de {{site.data.keyword.Bluemix}}, consulte [Cambio de planes de servicio](/docs/resources?topic=resources-changing){: external}.
