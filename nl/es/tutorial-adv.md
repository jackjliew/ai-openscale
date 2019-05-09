---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Guía de aprendizaje del SDK de Python (avanzada)
{: #crt-ov}

## Escenario
{: #crt-scenario}

Los prestamistas tradicionales se ven presionados a ampliar su cartera digital de servicios financieros a un público más amplio y diverso, lo que requiere un nuevo enfoque al modelado de riesgo crediticio. Sus equipos de ciencia de datos actualmente se basan en técnicas de modelado tradicionales, como árboles de decisión y regresión logística, que funcionan bien para conjuntos de datos moderados y realizan recomendaciones que se pueden explicar fácilmente. Esto satisface los requisitos normativos de que las decisiones sobre préstamos crediticios deben ser transparentes y explicables.

Para proporcionar acceso a crédito a una población más amplia y de mayor riesgo, las historias de crédito de los solicitantes deben expandirse más allá del crédito tradicional, como, por ejemplo, los créditos hipotecarios y los créditos para vehículos, a fuentes de créditos alternativas como las historias de pago de planes de telefonía móvil y servicios, así como a la formación y los puestos laborales. Estas nuevas fuentes de datos prometen, pero también añaden riesgo, puesto que aumenta la probabilidad de correlaciones inesperadas que introduzcan un sesgo según la edad, el sexo y otras características personales de los solicitantes.

Las técnicas de ciencia de datos más adecuadas para estos diversos conjuntos de datos, tales como los árboles de potenciación del gradiente y las redes neuronales, pueden generar modelos de riesgo precisos, pero con un coste. Estos modelos "de caja negra" generan predicciones opacas que de alguna manera deben ser transparentes, a fin de garantizar la aprobación normativa, como por ejemplo el Artículo 22 de la Regulación de Protección General de Datos (GDPR) o el Fair Credit Reporting Act (FCRA) del gobierno federal de Estados Unidos que gestiona el Consumer Financial Protection Bureau.

El modelo de riesgo crediticio que se proporciona en esta guía de aprendizaje utiliza un conjunto de datos de entrenamiento que contiene 20 atributos sobre cada solicitante de préstamo. Dos de estos atributos, edad y sexo, se pueden probar para comprobar si presentan algún sesgo. Para esta guía de aprendizaje, nos centraremos en el sesgo respecto a sexo y edad.

{{site.data.keyword.aios_short}} supervisará la propensión del modelo desplegado a un resultado favorable ("Sin riesgo") para un grupo (el grupo de referencia) respecto a otro (el grupo supervisado). En esta guía de aprendizaje, el grupo supervisado para sexo es `mujer`, mientras que el grupo supervisado por edad es `de 18 a 25`.

## Requisitos previos
{: #crt-prereqs}

Esta guía de aprendizaje utiliza un cuaderno Jupyter que se debe ejecutar en un proyecto de Watson Studio, utilizando un entorno de ejecución de "Python 3.5 con Spark". Requiere credenciales de servicio para los siguientes servicios de {{site.data.keyword.cloud_notm}}:

- Cloud Object Storage (para almacenar el proyecto de Watson Studio)
- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- (Opcional) Databases for PostgreSQL o Db2 Warehouse

El cuaderno Jupyter entrenará, creará y desplegará un modelo de riesgo crediticio alemán, configurará {{site.data.keyword.aios_short}} para supervisar ese despliegue y proporcionará medidas y registros históricos de un periodo de 7 días para su visualización en el panel de control Detalles de {{site.data.keyword.aios_short}}. También puede configurar opcionalmente el modelo para el aprendizaje continuo con Watson Studio y Spark.

## Introducción
{: #crt-intro}

En esta guía de aprendizaje, aprenderá a:

- Suministrar aprendizaje automático y servicios de almacenamiento de {{site.data.keyword.cloud_notm}}
- Configurar un proyecto de Watson Studio y ejecutar un cuaderno Python para crear, entrenar y desplegar un modelo de aprendizaje automático
- Ejecutar un cuaderno Python para crear una despensa de datos, configurar supervisores de rendimiento, exactitud y equidad y crear datos para supervisar
- Ver los resultados en la pestaña Detalles de {{site.data.keyword.aios_short}}

## Suministre servicios de {{site.data.keyword.cloud_notm}}
{: #crt-services}

Inicie sesión en la cuenta de [{{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}){: new_window} con su ID de IBM. Al suministrar servicios, especialmente en el caso de Db2 Warehouse, compruebe que su organización y espacio seleccionados son los mismos para todos los servicios.

### Cree una cuenta de Watson Studio
{: #crt-wstudio}

- [Cree una instancia de Watson Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/watson-studio){: new_window} si no tiene aún una asociada con la cuenta:

  ![Watson Studio](images/watson_studio.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

### Suministre un servicio de Cloud Object Storage
{: #crt-cos}

- [Suministre un servicio de Object Storage ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} si no tiene aún uno asociado con su cuenta:

  ![Object Storage](images/object_storage.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

### Suministre un servicio de Watson Machine Learning
{: #crt-wml}

- [Suministre una instancia de Watson Machine Learning ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/machine-learning){: new_window} si no tiene aún una asociada con la cuenta:

  ![Machine Learning](images/machine_learning.png)

- Dé un nombre al servicio, elija el plan Lite (gratuito) y pulse el botón **Crear**.

### (Opcional) Suministre un servicio Databases for PostgreSQL o DB2 Warehouse
{: #crt-db2}

Si tiene una cuenta de {{site.data.keyword.cloud_notm}} de pago, debe suministrar un servicio `Databases for PostgreSQL` o `Db2 Warehouse` para beneficiarse completamente de la integración con Watson Studio y los servicios de aprendizaje continuo. Si elige no suministrar un servicio de pago, puede utilizar el almacenamiento PostgreSQL interno gratuito con {{site.data.keyword.aios_short}}, pero no podrá configurar el aprendizaje continuo para el modelo.

- [Suministre un servicio de Databases for PostgreSQL![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/databases-for-postgresql) o [un servicio de Db2 Warehouse ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/catalog/services/db2-warehouse) si no tiene aún uno asociado con la cuenta:

  ![BD para Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Dé un nombre al servicio, elija el plan Standard (Databases for PostgreSQL) o el plan Entry (Db2 Warehouse) y pulse el botón **Crear**.

## Configure un proyecto de Watson Studio
{: #crt-set-wstudio}

- Inicie sesión en su [cuenta de Watson Studio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://dataplatform.ibm.com/){: new_window}. Pulse el icono de avatar de la cuenta en la esquina superior derecha y compruebe que la cuenta que utilice sea la misma cuenta que ha utilizado para crear los servicios de {{site.data.keyword.cloud_notm}}:

  ![Misma cuenta](images/same_account.png)

- En Watson Studio, empiece creando un nuevo proyecto. Seleccione "Crear un proyecto":

  ![Crear proyecto de Watson Studio](images/studio_create_proj.png)

- Seleccione el mosaico **Standard** para crear el proyecto:

  ![Seleccionar proyecto Standard de Watson Studio](images/studio_create_standard.png)

- Dé un nombre y una descripción al proyecto, asegúrese de que el servicio de Cloud Object Storage que ha creado esté seleccionado en el menú desplegable **Almacenamiento** y pulse **Crear**.

## Cree y despliegue un modelo de aprendizaje automático
{: #crt-make-model}

### Añada el cuaderno `Trabajar con Watson Machine Learning` al proyecto de Watson Studio
{: #crt-add-notebook}

- Descargue el archivo siguiente:

    - [Trabajar con Watson Machine Learning ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el botón **Añadir a proyecto** y seleccione **Cuaderno** en el menú desplegable:

  ![Añadir conexión](images/add_notebook.png)

- Seleccione **Desde archivo**:

  ![Nuevo formulario de cuaderno](images/new_notebook_name.png)

- A continuación, pulse el botón **Elegir archivo** y seleccione el archivo de cuaderno "german_credit_lab.ipynb" que ha descargado:

  ![Nuevo formulario de cuaderno](images/new_notebook_name2a.png)

- En la sección **Seleccionar tiempo de ejecución**, elija una opción Python 3.5 con Spark:

- Pulse **Crear cuaderno**.

### Edite y ejecute el cuaderno `Trabajar con Watson Machine Learning`
{: #crt-edit-notebook}

El cuaderno `Trabajar con Watson Machine Learning` contiene instrucciones detalladas de cada paso del código Python que ejecutará. A medida que avance en el cuaderno, dedique algún tiempo a comprender qué hace cada mandato.
{: tip}

- En la pestaña **Activos** del proyecto de Watson Studio, pulse el icono **Editar** junto al cuaderno `Trabajar con Watson Machine Learning` para editarlo.

- En la sección "Suministrar servicios y configurar credenciales", realice los cambios siguientes:

    - Siga las instrucciones para crear, copiar y pegar una clave de API de {{site.data.keyword.cloud_notm}}.

    - Reemplace las credenciales de servicio de Watson Machine Learning (WML) con las que ha creado previamente.

    - Reemplace las credenciales de BD con las que ha creado para Databases for PostgreSQL.

    - Si ha configurado anteriormente {{site.data.keyword.aios_short}} para utilizar una base de datos de PostgreSQL interna gratuita como despensa de datos, puede cambiar a una nueva despensa de datos que utiliza el servicio de Databases for PostgreSQL. Para suprimir la configuración anterior de PostgreSQL y crear una nueva, establezca la variable KEEP_MY_INTERNAL_POSTGRES en `False`.

        El cuaderno eliminará la despensa de datos de PostgreSQL interna existente y creará una nueva despensa de datos con las credenciales de base de datos proporcionadas. **No se producirá ninguna migración de datos**.
        {: important}

- Una vez que ha suministrado los servicios y especificado las credenciales, el cuaderno está listo para ejecutarse. Pulse el elemento de menú **Kernel** y seleccione **Reiniciar y borrar todo** en el menú:

  ![Reiniciar y borrar](images/restart_and_clear.png)

- Ahora ejecute secuencialmente cada uno de los pasos del cuaderno. Observe lo que sucede en cada paso, tal como se describe. Complete todos los pasos, hasta los pasos de la sección "Datos adicionales para ayudar en la depuración", estos incluidos.

El resultado neto es que habrá creado, entrenado y desplegado el modelo **Despliegue de riesgo alemán de Spark** en la instancia de servicio de {{site.data.keyword.aios_short}}. {{site.data.keyword.aios_short}} se configurará para comprobar si hay algún sesgo en el modelo respecto a sexo (en este caso, mujer) o edad (en este caso, de 18 a 25 años).

## Visualización de los resultados
{: #crt-view-results}

### Ver detalles del despliegue
{: #crt-view-insights}

Utilizando el panel de control de [{{site.data.keyword.aios_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, pulse en la pestaña **Detalles**:

  ![Detalles](images/insight-dash-tab.png)

La página Detalles proporciona una descripción general de las métricas para los modelos desplegados. Puede ver fácilmente las alertas de las métricas de Equidad o Exactitud que han caído por debajo del umbral establecido al ejecutar el cuaderno. Los datos y los valores utilizados en esta guía de aprendizaje habrán creado métricas de Exactitud y Equidad similares a las que se muestran aquí.

  ![Descripción general de Detalles](images/insight-overview-adv-tutorial-2.png)

### Ver datos de supervisión del despliegue
{: #crt-view-mon-data}

1. Para ver los detalles de supervisión, en la página **Detalles** pulse el mosaico correspondiente al despliegue. Aparecen los datos de supervisión de ese despliegue. 
2. Desplace el marcador por el gráfico para seleccionar los datos de la ventana de una hora específica. 
3. Pulse el enlace **Ver detalles**.

  ![Supervisar datos](images/insight-monitor-data2.png)

Ahora puede revisar en los gráficos los datos que ha supervisado. Para este ejemplo, puede ver que para la característica "Sexo", el grupo `mujer` ha recibido el resultado favorable "Sin riesgo" (68%) menor que el del grupo `hombre` (78%). 
  ![Descripción general de Detalles](images/insight-review-charts2.png)

### Vea la explicabilidad de una transacción de modelo
{: #crt-view-explain}

Para cada despliegue, puede ver los datos de explicabilidad de transacciones específicas.

Si ya sabe qué transacción desea ver, hay una forma rápida de buscarla con el ID de transacción. Después de pulsar en el archivo de despliegue, en el navegador, pulse el icono **Explicar una transacción** ![Pestaña Explicar una transacción](images/insight-transact-tab.png), especifique el ID de transacción y pulse **Intro**.
{: tip}

Si utiliza la versión Lite interna de PostgreSQL, es posible que no pueda recuperar las credenciales de la base de datos. Esto podría impedirle ver las transacciones.
{: note}

1. En los gráficos de los últimos datos sesgados, pulse el botón **Ver transacciones**.

  ![Ver transacciones](images/view_transactions.png)

  Aparece una lista de transacciones donde el despliegue ha actuado de forma sesgada. 
  
2. Seleccione una de las transacciones y, en la columna **ACCIÓN**, pulse el enlace **Explicar**.

  ![Lista de transacciones](images/transaction_list_cr.png)

Ahora verá una explicación de cómo el modelo ha llegado a esta conclusión, incluido el grado de seguridad del modelo, los factores que han contribuido al nivel de confianza y los atributos con los que se ha alimentado el modelo.

  ![Ver transacción](images/view_transaction_cr.png)
  
## Pasos siguientes
{: #crt-next-steps}

- Obtenga más información sobre cómo [ver e interpretar los datos](/docs/services/ai-openscale?topic=ai-openscale-it-ov) y [supervisar la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
