---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# Alta disponibilidad y recuperación tras desastre
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} tiene alta disponibilidad en diversas ubicaciones de {{site.data.keyword.cloud_notm}}, como Dallas y Washington, DC. Sin embargo, la recuperación tras posibles desastres que afecten a toda la ubicación requiere planificación y preparación.
{: shortdesc}

Usted es responsable de comprender la configuración, la personalización y el uso del servicio. También es responsable de estar preparado para volver a crear una instancia del servicio en una nueva ubicación y de restaurar los datos en cualquier ubicación. Consulte [¿Cómo puedo asegurar un tiempo de inactividad nulo?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external} para obtener más información.

## Alta disponibilidad 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} se despliega y está disponible en los centros de datos del sur de Estados Unidos (**us-south**) con direccionamiento multizona (MZR) en tres zonas de disponibilidad. En cualquier momento, si una zona no está disponible, el sistema continuará estando disponible en otras zonas de disponibilidad. El equilibrador de carga global y el servidor DNS direcciona el tráfico a las zonas disponibles sin ninguna interrupción para el usuario.

Los datos almacenados en las bases de datos de PostgreSQL también tienen alta disponibilidad y existen en diversas zonas de disponibilidad. Sin embargo, la responsabilidad del cliente es hacer copia de seguridad de los datos en soporte de un plan de recuperación ante desastres de manera que se puedan volver a crear los servicios.

Se realiza equilibrio de carga del tráfico de {{site.data.keyword.aios_short}} en varias zonas de una región. Cada zona es un centro de datos de la misma región. 

Periódicamente se hace copia de seguridad de las bases de datos compuestas, como las bases de datos PostgreSQL y de directorio distribuido <code>etc</code> (etcd) para garantizar la alta disponibilidad y, en caso de desastre, el equipo de operaciones de {{site.data.keyword.aios_short}} podrá recuperar el servicio en el Objetivo de punto de recuperación (RPO).
 
{{site.data.keyword.cloud_notm}} ofrece redundancia de datos en la región que permite la protección de alta disponibilidad. IBM proporciona réplica automática de datos para bases de datos de cliente que contienen datos de modelos personalizados o entrenamiento sin coste adicional. La réplica se completa en las zonas de disponibilidad de la región en los centros de datos de {{site.data.keyword.cloud_notm}}.
 
## Copia de seguridad y restauración
{: #openscale-restore}

Los clientes son responsables de realizar la copia de seguridad y la restauración de sus propios datos, incluidos los datos de modelos personalizados o entrenamiento así como los modelos personalizados generados por los clientes. Para ver las instrucciones sobre copia de seguridad y restauración para los clientes, consulte la documentación de {{site.data.keyword.cloud_notm}}.
 
## Recuperación tras desastre
{: #openscale-disaster-recovery}

La continuidad de negocio en la región se completa utilizando la réplica automática en las zonas de disponibilidad de la región en los centros de datos de {{site.data.keyword.cloud_notm}}. Los clientes son responsables de la recuperación tras desastre multiregión. Las responsabilidades incluyen la copia de seguridad, la restauración y la sincronización de sus propias políticas de seguridad, datos de modelos personalizados o entrenamiento y los modelos personalizados generados por los clientes. Además, el cliente es responsable del direccionamiento y el equilibrio de carga entre las regiones. Para ver las instrucciones sobre copia de seguridad y restauración, consulte la documentación de {{site.data.keyword.cloud_notm}}.
