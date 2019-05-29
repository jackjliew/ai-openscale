---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Creación de supervisores y métricas personalizados ![etiqueta beta](images/beta.png)
{: #cst_mtrcs}

Los supervisores personalizados consolidan un conjunto de métricas personalizadas que le permiten realizan un seguimiento, de forma cuantitativa, de cualquier aspecto del despliegue del modelo y de la aplicación empresarial. Puede definir métricas personalizadas y utilizarlas junto con las métricas estándar, como por ejemplo la calidad de modelo, el rendimiento o las métricas de imparcialidad que se supervisan en {{site.data.keyword.aios_full}}.
{: shortdesc}

Para gestionar las métricas y supervisores personalizados, debe utilizar la interfaz programática que forma parte del SDK de Python. De forma similar, puede almacenar métricas personalizadas en la despensa de datos de {{site.data.keyword.aios_short}} para acceder a ellas cuando sea necesario. Las métricas personalizadas también se visualizan en el panel de control de {{site.data.keyword.aios_short}}.

## Gestión de métricas personalizadas
{: #cst_mtrc_mgmt}

Para trabajar con métricas personalizadas, debe realizar las tareas siguientes:

1. Registrar el supervisor personalizado con la definición de métricas.
2. Habilitar el supervisor personalizado.
3. Almacenar valores de métrica.

En las siguientes guías de aprendizaje avanzado se muestra cómo hacerlo:

- [Trabajar con Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Trabajar con el motor de aprendizaje automático personalizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

Puede inhabilitar y habilitar de nuevo la supervisión personalizada en cualquier momento. Puede eliminar el supervisor personalizado si ya no lo necesita.

Para obtener más información, consulte la [documentación del SDK de Python](http://ai-openscale-python-client.mybluemix.net/).

## Acceder y visualizar métricas personalizadas
{: #cst_mtrcs_viz}

Para acceder a las métricas personalizadas y visualizarlas, puede utilizar la interfaz programática. En las siguientes guías de aprendizaje avanzado se muestra cómo hacerlo:

- [Trabajar con Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Trabajar con el motor de aprendizaje automático personalizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   Para obtener más información, consulte la [documentación del SDK de Python](http://ai-openscale-python-client.mybluemix.net/).

La visualización de las métricas personalizadas se puede encontrar también en el panel de control de Watson OpenScale.

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
