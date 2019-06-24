---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: feedback data, data, feedback, models

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

# Formato y carga de datos de opinión en {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

Los datos de opiniones son imprescindibles para mantener un modelo sin sesgo. Debe cargar regularmente los datos de opinión al servicio de {{site.data.keyword.aios_full}} para garantizar que el modelo tiene el cuenta los datos actualizados que pudieran indicar cambios en el contexto de la aplicación predictiva.  Con un bucle de opinión, el sistema aprende continuamente mediante la supervisión de la efectividad de las predicciones y el reentrenamiento, cuando así se requiere. La supervisión y la utilización de la opinión resultante son el núcleo del aprendizaje automático. La siguiente información está pensada para ayudarle con el formato y la carga de los datos de opinión.
(: shortdesc)

## Formato de los datos de opinión
{: #fmt-upld-fdbk-data-fmt}

Para leer correctamente los datos de opinión, estos se deben formatear correctamente. El servicio de {{site.data.keyword.aios_short}} acepta los formatos siguientes:

- Formatos de archivo CSV, que se pueden cargar mediante la interfaz de usuario o la API REST
- Formatos de archivo JSON, que solo se pueden cargar mediante la API REST

Estos formatos de archivos los define un esquema, `training_data_schema`, que está disponible en los detalles de suscripción. Para ver  `training_data_schema`, ejecute el mandato siguiente utilizando la API Python:

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Para comparar el esquema de datos de entrenamiento con el esquema de opinión, es posible que desee ver también el esquema de opinión. Para ver el esquema de opinión, ejecute el mandato siguiente utilizando la API Python:

```
subscription.feedback_logging.print_table_schema()
```


### Formato CSV
{: #fmt-upld-fdbk-data-fmt-csv}

Normalmente, para un archivo CSV proporciona los datos en columnas y filas con una fila para nombres de columna.

Normalmente no se requieren comillas cuando los nombres de columna están en mayúsculas, lo que hace que para Db2 no hay distinción de mayúsculas y minúsculas; sin embargo, para otras bases de datos y en la instancia donde los nombres de columna están en mayúsculas y minúsculas, estas deben coincidir.
Si el archivo contiene nombres de columna, estas no tienen que coincidir necesariamente con el orden de la tabla; sin embargo, si el archivo no tiene nombres de columna, sí que debe haber coincidencia. Es posible que tenga columnas que no estén en los datos de entrenamiento originales. Estas columnas se ignoran durante el proceso.


### Formato JSON
{: #fmt-upld-fdbk-data-fmt-json}

El formato JSON consta de una colección de objetos con campos correspondientes a los nombres de columna.

