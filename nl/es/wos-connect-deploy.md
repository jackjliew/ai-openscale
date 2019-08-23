---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: deployment, monitoring 

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

# Seleccionar despliegues para supervisar
{: #dpl-select}

Para añadir supervisores al panel de control de {{site.data.keyword.aios_short}}, debe tener modelos desplegados que estén disponibles mediante uno de los proveedores de aprendizaje automático configurados para {{site.data.keyword.aios_short}}. Selecciónelos en una lista de proveedores de aprendizaje automático y despliegues para supervisar.
{: shortdesc}

## Selección de despliegues
{: #dpl-config}

1.  En el panel de control de {{site.data.keyword.aios_short}}, pulse **Añadir a panel de control**.
1.  {{site.data.keyword.aios_short}} comprueba sus proveedores de aprendizaje automático para compilar una lista de los modelos desplegados. En la lista de despliegues, puede seleccionar aquellos que desee supervisar.

    ![Se muestra la ventana emergente Seleccionar despliegues con el proveedor de aprendizaje automático seleccionado y la lista de despliegues disponibles para ese proveedor](images/wos-select-model-deployment.png)

1.  Pulse **Configurar**.

Ha seleccionado correctamente los despliegues para supervisar. Ahora debe configurar los supervisores para este modelo. 

## Pasos siguientes
{: #dpl-next}

{{site.data.keyword.aios_short}} ahora está listo para que [configure supervisores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
