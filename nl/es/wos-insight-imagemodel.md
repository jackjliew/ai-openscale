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

# Explicación de los modelos de imagen
{: #ie-image}

{{site.data.keyword.aios_short}} da soporte a la explicabilidad para datos de imagen.
{: shortdesc}

## Cómo trabajar con un modelo de imagen
{: #ie-image-working}

1. Configure el entorno.
   2. Instale los paquetes de {{site.data.keyword.aios_short}} y {{site.data.keyword.pm_full}}.
   3. Configure sus credenciales.
   4. Instale las bibliotecas necesarias para crear los modelos y realizar el análisis. Incluyen las bibliotecas siguientes:
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. Cree y despliegue el modelo basado en imagen.
   2. Cree carpetas para las imágenes en función de cómo las clasifique.
       - En el directorio `data` principal debe tener los subdirectorios `train` y `validation`.
       - En cada uno de los subdirectorios debe tener sus directorios de clasificación.
  2. Estandarice el tamaño de la imagen y, a continuación, establezca los directorios que se utilizarán para el entrenamiento y la validación.
  3. Preprocese los datos para reescalar y recuperar las imágenes y sus clases.
  4. Defina y entrene el modelo.
  5. Almacene el modelo.
  6. Despliegue el modelo.

7. Configure {{site.data.keyword.aios_short}} asignando `APIClient`, suscribiendo el activo y puntuando el modelo.
8. Configure la explicabilidad.
   9. Habilite la explicabilidad.
   10. Obtenga explicaciones de las transacciones.
   11. Visualice las imágenes explicadas. 

## Explicación de las transacciones de modelos de imagen
{: #ie-image-workingviewing}

Para un ejemplo de explicabilidad de modelo de clasificación de imagen, puede ver qué partes de una imagen han contribuido positivamente al resultado previsto y cuáles han contribuido negativamente. En
el ejemplo siguiente, la imagen en el panel positivo muestra las partes que han afectado positivamente a la predicción y la imagen en el panel negativo
muestra las partes de las imágenes que han tenido un impacto negativo en el resultado.

![Se muestran los detalles de confianza de clasificación de imágenes de explicabilidad con una imagen de un perro que también tiene partes de la imagen resaltadas para mostrar qué parte de la imagen ha ayudado a determinar que la imagen es un perro](images/insight-explain-image.png)

Para {{site.data.keyword.pm_full}}, la entrada de puntuación para los modelos de clasificación de imagen que se envían para el registro de carga útil no puede exceder de 1 MB. Para evitar problemas de tiempo de espera excedido, las imágenes no deben sobrepasar 125 x 125 píxeles y se deben enviar secuencialmente de forma que se solicite la explicación de la segunda imagen cuando se haya completado la primera.
{: note}


## Ejemplos de modelo de imagen
{: #ie-image-working-ntbks}

Utilice los dos cuadernos siguientes para ver ejemplos de código detallados y desarrollar sus propios despliegues de {{site.data.keyword.aios_short}}:

- [Guía de aprendizaje para generar una explicación para un modelo basado en imagen](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Guía de aprendizaje para generar una explicación para un modelo de clasificador binario basado en imágenes](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

