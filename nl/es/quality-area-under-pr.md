---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# Área bajo PR ![etiqueta beta](images/beta.png)
{: #quality-area-pr}

El área bajo exhaustividad de precisión proporciona el área bajo la curva de precisión y exhaustividad, lo que puede ser útil cuando las clases estén especialmente desequilibradas.
{: shortdesc}

## Detalles del área bajo PR
{: #quality-area-pr-glance}

- **Descripción**: área bajo precisión y curva de exhaustividad
- **Umbrales predeterminados**: límite inferior = 80%
- **Recomendación predeterminada**:
   - **Tendencia al alza**: una tendencia al alza indica que la métrica está mejorando. Esto significa que el reentrenamiento del modelo es efectivo.
   - **Tendencia a la baja**: una tendencia a la baja indica que la métrica se está deteriorando. Los datos de opinión son ligeramente diferentes a los datos de entrenamiento.
   - **Variación errática o irregular**: una variación errática o irregular indica que los datos de opinión no son coherentes entre evaluaciones. Incremente el tamaño mínimo de la muestra para el supervisor de calidad.
- **Tipo de problema**: clasificación binaria
- **Valores de gráfico**: último valor en el margen de tiempo
- **Detalles de métricas disponibles**: Confusion Matrix

## Interpretación de la pantalla
{: #quality-area-pr-display}

![Se muestra Área bajo PR con tendencia de métricas descendente](images/quality-area-under-pr.png)


## Cómo calcularlo
{: #quality-area-pr-math}

Área bajo exhaustividad de precisión proporciona el total de `Precisión + Exhaustividad`.

La precisión (P) se define como el número de verdaderos positivos (Tp) sobre el número de verdaderos positivos más el número de falsos positivos (Fp).

```
               número de verdaderos positivos
Precisión =   ______________________________________________________

              (número de verdaderos positivos + número de falsos positivos)
```

La exhaustividad (R) se define como el número de verdaderos positivos (Tp) sobre el número de verdaderos positivos más el número de falsos negativos (Fn).

```
                  número de verdaderos positivos
Exhaustividad =   ______________________________________________________

                  (número de verdaderos positivos + número de falsos negativos)
```
