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

# Visualización de los datos para un despliegue
{: #it-vdep}

Seleccione un despliegue desde el panel de control para ver los datos de supervisión para ese despliegue. La cabecera muestra información sobre el modelo desplegado, como por ejemplo los campos **ID de modelo** y **Fecha de creación**.
{: shortdesc}

![Se muestra una serie de tiempo con las horas de un día y una puntuación de equidad](images/insight-time-chart.png)

Puesto que las comprobaciones de algoritmo se ejecutan solo cada hora, también se proporcionan algunos enlaces para comprobar la equidad y la calidad bajo demanda. En el panel **Planificación**, puede pulsar los enlaces siguientes para realizar una comprobación inmediata de los datos:

![Se muestra el botón Comprobar equidad](images/wos-fairness-button.png)


![Se muestra el botón Comprobar calidad](images/wos-quality-button.png)

A continuación, pulse en el gráfico y mueva el marcador por el gráfico para ver las estadísticas de una hora individual:

![Se muestran los detalles del gráfico de series de tiempo con un punto de datos específico en el gráfico seleccionado y una ayuda contextual que indica que pulse para ver los detalles](images/wos-insight-time-detail.png)

- ***Equidad***: dos características de equidad, Sexo y Edad, han cumplido sus umbrales establecidos para la aprobación.
- ***Calidad***: la métrica **Área bajo ROC** muestra una alerta porque no estaba dentro del umbral configurado.
- ***Prom. req/mín***: pulse la métrica **Productividad** para ver el número de registros procesados por minuto. La productividad se calcula cada minuto, y se informa en el gráfico de su valor promedio en el curso de la hora.


## Ver transacciones
{: #it-tra}

Esta opción le permite ver las transacciones individuales que han contribuido al sesgo al pulsar el botón **Ver transacciones**.

![Se muestra el botón Ver transacciones](images/view_transactions.png)

Aparece una lista de transacciones donde el despliegue ha tenido un comportamiento sesgado. Pulse el enlace **Explicar** para cualquiera de los ID de transacción para obtener información detallada sobre esa transacción en la pestaña Explicabilidad. Para obtener más información, consulte [Supervisión de la explicabilidad](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Seleccione la vista **Todas las transacciones** para ver todas las transacciones de la característica seleccionada (en este ejemplo "EDAD") y el periodo seleccionado (en este ejemplo "15 de septiembre de 2018 a las 1:00 PM"):

![Transacción lista todas las transacciones para un punto de datos específico](images/transaction_list1.png)

Seleccione la vista **Transacciones sesgadas** para ver sólo el subconjunto de transacciones que ha recibido los resultados sesgados. Cada transacción sesgada se compara con una transacción similar pero ligeramente modificada (perturbada) que muestra cómo el cambio del valor de la característica supervisada (EDAD) producirá un resultado favorable para la transacción sesgada:

![Transacción lista solo las transacciones sesgadas](images/transaction_list2.png)


