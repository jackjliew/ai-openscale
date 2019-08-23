---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Configuración del supervisor de detección de desviación ![etiqueta beta](images/beta.png)
{: #behavior-drift-config}

Para poder empezar a analizar su modelo, primero debe configurar el supervisor de desviación de {{site.data.keyword.aios_full}}. Existen dos opciones: entrenar el modelo en línea o bien utilizar un cuaderno.
{: shortdesc}

Puede entrenar el modelo en línea mediante {{site.data.keyword.aios_short}}
si utiliza {{site.data.keyword.pm_full}} y sus datos no superan los 500 MB. De lo contrario, debe utilizar un cuaderno para entrenar el modelo.

## Pasos para configurar la desviación en {{site.data.keyword.aios_short}}
{: #behavior-drift-config-steps-wos}

Si utiliza {{site.data.keyword.pm_full}}, tiene la opción de utilizar la interfaz de usuario de {{site.data.keyword.aios_short}} para configurar la detección de desviación.

1. En la pestaña **Desviación**, en la página **¿Qué es desviación?**, pulse **Iniciar** para iniciar el proceso de configuración.

   ![Página ¿Qué es desviación?](images/wos-drift-config-1.png)

2. Pulse el mosaico **Entrenar en Watson OpenScale**.

   ![Página ¿Qué es desviación?](images/drift-config-2.png)

3. Establezca el umbral de alerta.

   ![Página ¿Qué es desviación?](images/drift-config-3.png)

3. Establezca el tamaño de la muestra.

   ![Página ¿Qué es desviación?](images/drift-config-4.png)
   
3. Pulse **Guardar**.


## Pasos para configurar la desviación utilizando un cuaderno
{: #behavior-drift-config-steps-ntbk}

Si utiliza un proveedor de aprendizaje automático que no sea {{site.data.keyword.pm_full}}, como Microsoft Azure, Amazon SageMaker o un motor de aprendizaje automático personalizado, debe utilizar un cuaderno para configurar la detección de desviación. También es posible configurar la desviación para {{site.data.keyword.pm_full}} mediante este método.

Esta opción es útil si los datos de entrenamiento no se almacenan en Db2 ni {{site.data.keyword.cos_full}}. Utilizando un cuaderno, debe leer los datos de entrenamiento en un marco de datos. El cuaderno especializado que puede descargar de {{site.data.keyword.aios_short}} crea a continuación una salida especializada que puede cargar a {{site.data.keyword.aios_short}}.

1. Cree un cuaderno para generar el modelo de detección de desviación. Utilice [el cuaderno de ejemplo](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb) que está disponible en la interfaz de usuario de {{site.data.keyword.aios_short}}.
2. Utilice software de compresión para comprimir el modelo de detección de desviación en un archivo .tar.gz.

1. En la pestaña **Desviación**, en la página **¿Qué es desviación?**, pulse **Iniciar** para iniciar el proceso de configuración.

   ![Página ¿Qué es desviación?](images/wos-drift-config-1.png)

2. Pulse el mosaico **Entrenar en un cuaderno**.

   ![Página de configuración de desviación con una opción en línea y una opción de cuaderno](images/drift-config-2.png)

3. Arrastre el archivo del modelo comprimido a la zona de destino, o examine para seleccionarlo y pulse **Siguiente**.

   ![Página ¿Qué es desviación?](images/wos-drift-config-2b.png)
   
3. Cargue el modelo de detección de desviación y pulse **Siguiente**.

   ![Página ¿Qué es desviación?](images/drift-config-upload.png)
   
3. Establezca el umbral de alerta.

   ![Página ¿Qué es desviación?](images/drift-config-3.png)

3. Establezca el tamaño de la muestra.

   ![Página ¿Qué es desviación?](images/drift-config-4.png)
   
3. Pulse **Guardar**.

## Pasos siguientes
{: #behavior-drift-config-next-steps}

- Para obtener más información sobre cómo interpretar la desviación, consulte [Magnitud de la desviación](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
