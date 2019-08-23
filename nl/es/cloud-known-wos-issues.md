---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Problemas conocidos y limitaciones de {{site.data.keyword.aios_short}} para {{site.data.keyword.cloud_notm}}
{: #rn-12ki}

Las listas siguientes contienen los problemas conocidos y la limitación que son comunes para {{site.data.keyword.aios_full}} para {{site.data.keyword.Bluemix}} y {{site.data.keyword.wos4d_full}} y también los que son específicos de  {{site.data.keyword.aios_full}} para {{site.data.keyword.Bluemix}}.
{: shortdesc}

<p>&nbsp;</p>

## Problemas comunes
{: #wos-common-issues}

Las limitaciones y los problemas conocidos siguientes son comunes a {{site.data.keyword.aios_full}} en {{site.data.keyword.Bluemix}} y {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### Limitaciones comunes
{: #wos-limitations}

- Para {{site.data.keyword.pm_full}}, la entrada de puntuación para los modelos de clasificación de imagen que se envían para el registro de carga útil no puede exceder de 1 MB. Para evitar problemas de tiempo de espera excedido, las imágenes no deben sobrepasar 125 x 125 píxeles y se deben enviar secuencialmente de forma que se solicite la explicación de la segunda imagen cuando se haya completado la primera.


- La explicabilidad para modelos de texto no estructurados no está soportada para los lenguajes de script continuos como, por ejemplo, japonés, chino y coreano, que no utilizan espacios en blanco o caracteres de puntuación para separar las palabras.



<p>&nbsp;</p>


### Errores de configuración de la desviación impiden la configuración del supervisor de desviación
{: #wos-common-issues-mismatchdatatype}

La flexibilidad de la pantalla de configuración del modelo también puede causar problemas posteriormente cuando se desee configurar supervisores, como por ejemplo el supervisor de detección de desviación. Puesto que puede elegir los tipos de datos, debe asegurarse de que sus selecciones reflejan lo que es original del modelo. El error siguiente se puede producir si no se selecciona el tipo de columna de predicción adecuado:

```
"error": AIQDS2003E",
"message": "Las predicciones del modelo '[0. 1.]' son distintas de los nombres de clase en los datos de entrenamiento '['No' 'Yes']' para la suscripción <<número>> en la despensa de datos <<ID de despensa de datos>> y el enlace de servicio <<ID de enlace>>.
```

Los casos siguientes son la causa más probable:

- La etiqueta `class` es de tipo serie y se asigna `modeling_role` **prediction** a la columna **prediction** como tipo doble porque así es cómo se define el esquema de datos de salida.
- Selecciona la columna **prediction** de tipo doble en la interfaz de usuario, lo que no está restringido.


### Formatos de carga útil
{: #wos-common-issues-payloadformat}

Para procesar correctamente el análisis de carga útil, {{site.data.keyword.aios_short}} no da soporte a nombres de columna con comillas dobles (") en la carga útil. Esto afecta a la carga útil de puntuación y a los datos de opinión en los formatos CSV y JSON.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- De los dos tipos de servicios web de Azure Machine Learning, {{site.data.keyword.aios_short}} sólo admite el tipo `Nuevo`. El tipo `Clásico` no se admite.

- __*Se debe utilizar el nombre de entrada predeterminado*__: en el servicio web de Azure, el nombre de entrada predeterminado es `"input1"`. Actualmente, este campo se establece para {{site.data.keyword.aios_short}} y, si falta, {{site.data.keyword.aios_short}} no funcionará.

  Si el servicio web de Azure no utiliza el nombre predeterminado, cambie el nombre de campo de entrada a `"input1"` y el código funcionará.

- Si las llamadas a Microsoft Azure ML Studio para listar los modelos de aprendizaje automático provocan que la respuesta exceda el tiempo de
espera, por ejemplo, cuando tiene muchos servicios web, debe aumentar los valores de tiempo de espera. Por ejemplo, si utiliza el equilibrador de carga
HAProxy, es posible que tenga que trabajar en torno a este problema emitiendo los mandatos siguientes:

   - Inicie sesión en el equilibrador de carga y actualice `/etc/haproxy/haproxy.cfg` para establecer el tiempo de espera de cliente y servidor de `1m` a `5m`:

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - Ejecute `systemctl restart haproxy` para reiniciar el equilibrador de carga HAProxy.

Si utiliza otro equilibrador de carga, que no sea HAProxy, es posible que deba ajustar los valores de tiempo de espera de forma similar.
      {: note}

- De los dos tipos de servicios web de Azure Machine Learning, {{site.data.keyword.aios_short}} sólo admite el tipo `Nuevo`. El tipo `Clásico` no se admite.

- En el servicio web de Azure, el nombre de entrada predeterminado es `"input1"`. Actualmente, este campo es obligatorio para
{{site.data.keyword.aios_short}} y, si falta, la supervisión de exactitud falla.

   Si el servicio web de Azure no utiliza el nombre predeterminado, cambie el nombre de campo de entrada por `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*No se da soporte al algoritmo BlazingText*__: en el release actual de {{site.data.keyword.aios_short}},
no se da soporte al formato de carga útil de entrada de algoritmo BlazingText de AWS SageMaker.

<p>&nbsp;</p>


### Instancia de servicio de aprendizaje automático personalizado
{: #wos-common-issues-custom}

- El [módulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) actualmente no tiene Explicabilidad operativa para la instancia de servicio personalizado. Esto se debe a que la instancia de servicio personalizado requiere una predicción numérica en los datos de respuesta, que no se incluye con el script de módulo.

<p>&nbsp;</p>


- **Fragmentos de código no válidos**

    - Los fragmentos de código cURL y Python proporcionados para la configuración del supervisor no son válidos. Corrija los fragmentos de código que se proporcionan aquí:

      *Registro de carga útil*

      ```cURL
      # Generar una señal de acceso ICP pasando un nombre de usuario de ICP como $USERNAME y la contraseña ICP como $PASSWORD en la solicitud siguiente

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la solicitud de CURL anterior devolverá una señal de autenticación bajo "accessToken", que utilizará como {icp_token} en la siguiente
      solicitud de registro de carga
      # TODO: definir y pasar manualmente:
      # request - entrada en punto final de puntuación soportado por el formato de {{site.data.keyword.aios_short}} - sustituir campos de ejemplo
y valor por unos apropiados
      # response - salida de modelo puntuado soportado por el formato de {{site.data.keyword.aios_short}} - sustituir campos y valor de ejemplo
por unos adecuados
      # - $SCORING_ID - ID de la transacción de puntuación
      # - $SCORING_TIME - Tiempo necesario (ms) para realizar la predicción (para supervisión de rendimiento)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["EDAD", "SEXO", "BP", "COLESTEROL", "NA", "K"],
          "values": [[28, "F", "BAJO", "ALTO", 0.61, 0.026]]
      },
      "response": {
        "fields": ["EDAD", "SEXO", "BP", "COLESTEROL", "NA", "K", "probabilidad", "predicción", "FÁRMACO"],
        "values": [[28, "F", "BAJO", "ALTO", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "fármacoY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Registro de opiniones*

      ```cURL
      # Generar una señal de acceso ICP pasando un nombre de usuario de ICP como $USERNAME y la contraseña ICP como $PASSWORD en la solicitud siguiente

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la solicitud de CURL anterior devolverá una señal de autenticación bajo la clave "accessToken" que utilizará como {icp_token} en
la solicitud de registro de carga útil siguiente
      # TODO: definir manualmente y pasar:
      # fields - lista de nombres de campo - sustituir valores de ejemplo por los adecuados                                                       # values -
      # values - registro de datos de comentarios - sustituir valores de ejemplo por los adecuados
      # - $SCORING_ID - ID de la transacción de puntuación
      # - $SCORING_TIME - Tiempo necesario (ms) para realizar la predicción (para supervisión de rendimiento)

      FEEDBACK_DATA='{
        "fields": ["EDAD", "SEXO", "BP", "COLESTEROL", "NA", "K", "FÁRMACO"],
        "values": [[28, "F", "BAJO", "ALTO", 0.61, 0.026, "fármacoB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - El fragmento de código Java proporcionado para la eliminación del sesgo del punto final no es válido. Corrija el fragmento de código que se proporciona aquí:

      *Eliminar sesgo de punto final*

      ```java
      /**
      En tiempo de ejecución debe reemplazar los valores por los siguientes

      <HOSTNAME> - Nombre de host, p.ej.: aiopenscale.test.cloud.ibm.com
      <PORT> - Puerto del servidor
      <DATA_MART_ID> - ID de despensa de datos
      <SERVICE_BINDING_ID> - ID de enlace de servicio
      <ASSET_ID> - ID de activo o ID de modelo
      <DEPLOYMENT_ID> - ID de despliegue
      <TOKEN> - Señal portadora

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


### Soporte de navegadores
{: #abt-browser}

Las herramientas del servicio de {{site.data.keyword.aios_short}} requieren el mismo nivel de software del navegador que requiere {{site.data.keyword.cloud_notm}}. Consulte el tema {{site.data.keyword.cloud_notm}} [Requisitos previos](/docs/overview?topic=overview-prereqs-platform#browsers) para obtener más detalles.

<p>&nbsp;</p>


### Cliente Python
{: #abt-python}

El cliente de Python de
[{{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} es una biblioteca de Python
que le permite trabajar directamente con el servicio de {{site.data.keyword.aios_short}}. Puede utilizar el cliente de Python, en lugar de la
interfaz de usuario de cliente de {{site.data.keyword.aios_short}}, para configurar directamente la base de datos de despensa de datos, enlazar el motor de aprendizaje automático y
seleccionar y supervisar despliegues. Para ver los ejemplos que utilizan el cliente de Python de esta forma, consulte los
[cuadernos de ejemplo de {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).


## Problemas específicos de {{site.data.keyword.aios_short}}
{: #cloud-issues}

La limitación y los problemas siguientes son específicos de {{site.data.keyword.aios_short}} para {{site.data.keyword.Bluemix}}.

<p>&nbsp;</p>

### Limitaciones
{: #cloud-limitations}

- El release actual sólo da soporte a una base de datos, a una instancia de {{site.data.keyword.pm_full}} y a una instancia de{{site.data.keyword.aios_short}}. 

- La base de datos y la instancia de {{site.data.keyword.pm_full}} se deben desplegar en la misma cuenta de {{site.data.keyword.cloud_notm}}.

- {{site.data.keyword.aios_short}} utiliza la base de datos PostgreSQL o Db2 para almacenar datos relacionados con modelos (datos de opinión, carga útil de puntuación) y métricas calculadas. Actualmente no se da soporte a los planes Lite Db2.

- La base de datos del plan gratuito de Lite no es compatible con GDPR. Si el modelo procesa información de identificación personal (PII), debe
adquirir una nueva base de datos o utilizar una base de datos existente que cumpla la normativa GDPR.



<p>&nbsp;</p>
## Pasos siguientes
{: #abt-next}

- [Cómo empezar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- Vea el [material de referencia de API](https://{DomainName}/apidocs/ai-openscale){: external}.
- [Novedades de {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Contactar con IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
