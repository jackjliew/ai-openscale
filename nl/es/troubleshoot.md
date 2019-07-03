---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: troubleshooting, bias

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

# Resolución de problemas
{: #ts-trouble}

## Problemas comunes de {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

Los problemas siguientes son comunes a {{site.data.keyword.aios_full}} on Cloud y {{site.data.keyword.wos4d_full}}.

### Análisis de carga útil no se visualiza correctamente
{: #ts-trouble-common-payloadfileformat}

- Situación: Aparece el siguiente mensaje de error:
  - código de error: AIQDT0044E
  - texto del error: Carácter prohibido `"` en el nombre de columna `<column name>`

- Situación: Para procesar correctamente el análisis de carga útil, {{site.data.keyword.aios_short}} no da soporte a nombres de columna con comillas dobles (") en la carga útil. Esto afecta a la carga útil de puntuación y a los datos de opinión en los formatos CSV y JSON.
- Solución: Elimine las comillas dobles (") de los nombres de columna del archivo de carga útil.

## Problemas específicos de {{site.data.keyword.wos4d_full}}
{: #ts-trouble-icp}

Los problemas siguientes son específicos de {{site.data.keyword.wos4d_full}}:

## El servicio de sesgo/equidad está inactivo
{: #ts-bfdown}

### Descripción general
{: #ts-bfdov}

- Situación: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-bfdck}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-bfdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NOMBRE                                                       LISTO      ESTADO  REINICIOS   EDAD
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       En ejecución  0      2h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **2/2**.  Utilizaremos
`ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o <format>. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

    - Asegúrese de que tiene el nombre de imagen correcto.
    - ¿Ha enviado la imagen al repositorio?
    - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Puesto que este pod tiene 3 contenedores, aios-bias, ml-gateway-sidecar y check-etcd-ready, también debería comprobar el registro de ml-gateway-sidecar y check-etcd-ready si aios-bias no presenta ningún problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    En general, los registros deben contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información de los registros.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---
## El servicio de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosdown}

### Descripción general
{: #ts-odov}

- Situación: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil. . .
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-odkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}

    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-odvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NOMBRE                                                        LISTO      ESTADO   REINICIOS   ANTIGÜEDAD
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1    En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

        Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

        - Añadir más nodos al clúster.

        - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
        ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
        ```

        - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

        - Asegúrese de que tiene el nombre de imagen correcto.
        - ¿Ha enviado la imagen al repositorio?
        - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---
## El servicio de configuración de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosconfigdown}

### Descripción general
{: #ts-ocdov}

- Situación: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-ocdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-ocdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NOMBRE                                                   LISTO     ESTADOS  REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1     En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-configuration-554f548667-7l782` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio del panel de control de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosdashdown}

### Descripción general
{: #ts-oddov}

- Situación: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: N/D

### Configurar kubectl
{: #ts-oddkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-oddvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NOMBRE                                                      LISTO      ESTADOS    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1      En ejecución   0          4h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---
## El servicio de despensa de datos está inactivo
{: #ts-datamartdown}

### Descripción general
{: #ts-dmdov}

- Situación: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-dmdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-dmdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NOMBRE                                                        LISTO      ESTADO   REINICIOS   ANTIGÜEDAD
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1     En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de explicabilidad está inactivo
{: #ts-expdown}

### Descripción general
{: #ts-esdov}

- Situación: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-esdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-esdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NOMBRE                                                       LISTO      ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       En ejecución   0          4h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **2/2**.  Utilizaremos
`ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Puesto que este pod tiene 3 contenedores, explainability-service, ml-gateway-sidecar y check-etcd-ready, también debería comprobar el registro de ml-gateway-sidecar y check-etcd-ready si explainability-service no presenta ningún problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      En general, los registros deben contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información de los registros.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de opinión de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosfeedbackdown}

### Descripción general
{: #ts-fsdov}

- Situación: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: etcd

### Configurar kubectl
{: #ts-fsdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-fsdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NOMBRE                                                         LISTO     ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2    En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **2/2**.  Utilizaremos
`ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Debido a que este pod tiene 3 contenedores, aios-feedback, ml-gateway-sidecar y check-etcd-ready, también debe echar un vistazo al registro de ml-gateway-sidecar y check-etcd-ready-ready si aios-feedback no tiene ningún problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      En general, los registros deben contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información de los registros.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de descubrimiento de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosdiscdown}

### Descripción general
{: #ts-dsdov}

- Situación: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: N/D

### Configurar kubectl
{: #ts-dsdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Opción 2: Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-dsdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NOMBRE                                                         LISTO     ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1     En ejecución  1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio nginx de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosnginxdown}

### Descripción general
{: #ts-nsdov}

- Situación: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: N/D

### Configurar kubectl
{: #ts-nsdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-nsdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NOMBRE                                                        LISTO     ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1     En ejecución   0          4h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de API de registro de carga útil de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiospayloadapidown}

### Descripción general
{: #ts-pladov}

- Situación: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden escribir carga útil en nuestro servicio desde servicios externos (Azur, Amazon u otro) por lo que no tienen los datos actuales para analizar.
- Sistema de supervisión:
- Dependencias: IBM Event Stream

### Configurar kubectl
{: #ts-pladkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-pladvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NOMBRE                                                        LISTO      ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1    En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o <format>. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de registro de carga útil de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiospayloaddown}

### Descripción general
{: #ts-plsdov}

- Situación: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden escribir carga útil en nuestro servicio desde servicios externos (Azur, Amazon u otro) por lo que no tienen los datos actuales para analizar.
- Sistema de supervisión:
- Dependencias: IBM Event Stream

### Configurar kubectl
{: #ts-plsdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-plsdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NOMBRE                                                         LISTO     ESTADO   REINICIOS   ANTIGÜEDAD
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1     En ejecución   1          6h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o <format>. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de planificación de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosscheddown}

### Descripción general
{: #ts-ssdov}

- Situación: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: N/D

### Configurar kubectl
{: #ts-ssdkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}`:8443
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-ssdvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NOMBRE                                                        LISTO     ESTADO    REINICIOS  ANTIGÜEDAD
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1     En ejecución   0          2h
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio redis de {{site.data.keyword.aios_short}} está inactivo
{: #ts-aiosredisdown}

### Descripción general
{: #ts-redov}

- Situación: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: N/D

### Configurar kubectl
{: #ts-redkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-redvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    NOMBRE                                                        LISTO     ESTADO    REINICIOS   ANTIGÜEDAD
    aios-redis-sentinel-6d5bffbcd8-hjvgk                          1/1     En ejecución    0          14m
    aios-redis-sentinel-6d5bffbcd8-j4htd                          1/1     En ejecución    0          14m
    aios-redis-sentinel-6d5bffbcd8-w4vcb                          1/1     En ejecución    0          14m
    aios-redis-server-6f4c55fd75-h4nfh                            1/1     En ejecución    0          14m
    aios-redis-server-6f4c55fd75-k9ggw                            1/1     En ejecución    0          14m
    aios-redis-server-6f4c55fd75-nlrr4                            1/1     En ejecución    0          14m
    ```

    Asegúrese de que el estado sea **en ejecución** y de que esté completamente listo **1/1**.  Utilizaremos
`aios-redis-server-6f4c55fd75-nlrr4` como nuestro pod para los ejemplos siguientes.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o <format>. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## El servicio de etcd está inactivo
{: #ts-etcddown}

### Descripción general
{: #ts-etcov}

- Situación: etcd_micro_service_is_down:
- Impacto en los clientes: los clientes no pueden utilizar ninguna funcionalidad como por ejemplo configurar instancias nuevas, análisis de solicitudes, almacenar carga útil...
- Sistema de supervisión:
- Dependencias: ninguna

### Configurar kubectl
{: #ts-etckc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Pasos de verificación/recuperación
{: #ts-etcvr}

1.  Compruebe el estado del pod con los mandatos siguientes:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    NOMBRE                                       LISTO     ESTADO          REINICIOS      ANTIGÜEDAD
    etcd-0                                       1/1     En ejecución          3          8d
    etcd-1                                       1/1     En ejecución          0          8d
    etcd-2                                       1/1     En ejecución          0          8d
    ```

    Asegúrese de que haya tres pods etcd, que su estado sea **en ejecución** y que estén totalmente listos **1/1**.

1.  Describa el pod si este no está en la etapa de ejecución:

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    Este mandato mostrará los detalles del pod.  Esto también proporciona errores si el pod no está en la etapa de ejecución.  Es posible que el
pod encuentre los casos siguientes cuando no se esté ejecutando la etapa:

    - **Mi pod permanece pendiente**

      Si el pod permanece **Pendiente**, significa que no se puede planificar a un nodo.  Normalmente esto sucede porque no hay recursos suficientes de un tipo u otro que impiden la planificación.  Ejecute el mandato anterior para obtener más información. Debería haber mensajes del planificador sobre el motivo por el que no puede planificar el pod. Es posible que haya agotado el suministro de CPU o memoria en el clúster. En este caso, puede probar varias acciones:

      - Añadir más nodos al clúster.

      - Terminar los pods no necesarios para hacer espacio para los pods pendientes.
      ```bash
      kubectl -n [espacio de nombres] delete pod [nombre de pod]
      ```

      - Compruebe que el tamaño del pod no sea mayor que el tamaño de sus nodos. Por ejemplo, si todos los nodos tienen una capacidad de cpu:1, un pod con una solicitud de cpu: 1.1 no se planificará nunca.

      Puede comprobar las capacidades de nodo con el mandato kubectl get nodes -o `<format>`. A continuación se muestran algunos mandatos de ejemplo que extraen sólo la información necesaria:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mi pod permanece en espera**

      Si un pod está atascado en el estado **En espera**, se ha planificado a un nodo de trabajador, pero no se puede ejecutar en esa máquina. De nuevo, la información de kubectl describe ... debería ser útil. La causa más común de pods **En espera** es un error al obtener la imagen. Compruebe los tres puntos siguientes:

      - Asegúrese de que tiene el nombre de imagen correcto.
      - ¿Ha enviado la imagen al repositorio?
      - Ejecute una `obtención de docker` manual para obtener la imagen en el clúster y comprobar que la imagen se puede obtener.

    - **Mi pod se cuelga o está en otro estado incorrecto**

      En primer lugar, compruebe los registros del contenedor actual:
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      Si el contenedor se había colgado anteriormente, puede acceder al registro de bloqueo del contenedor anterior con:
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      En general, el registro debe contener información sobre el motivo por el que el pod no se ha iniciado correctamente.  Corrija el problema según la información del registro.  Si ninguno de estos enfoques funciona, continúe con los pasos de Escalamiento.

---

## Crear un panel de control con event_stream
{: #ts-createdashes}

### Descripción general
{: #ts-dshov}

- En este documento se describe cómo crear un nuevo panel de control para supervisar servicios de {{site.data.keyword.aios_full}}.

### Configurar kubectl
{: #ts-dshkc}

Hay dos maneras de configurar el cliente kubectl.

1.  Mediante la herramienta cloudctl

    Si cloudctl está disponible en su portátil, ejecute el mandato siguiente para configurar kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    Sustituya `${username}`, `${password}` y `${ICP Host}` por su valor real.  Por ejemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Utilización de la configuración kubectl de la consola de {{site.data.keyword.icpfull}}
    - Inicie sesión en el clúster de {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Seleccione el icono de **persona redonda** > **Configurar cliente**
    - Pulse en el icono **Copiar al Portapapeles** para copiar la información de configuración en el portapapeles
    - Cambie el espacio de nombres de `aiopenscale` a `es` si es necesario.
    - Pegue la información de configuración en la línea de mandatos y pulse **Intro**.

### Visualización de la secuencia de sucesos
{: #ts-dshve}

La secuencia de sucesos consta de varios servicios.  Consulte la subcarpeta para ver los detalles de cada servicio.

  ```bash
  $ kubectl get pods -n eventstream
  NOMBRE                                                LISTO     ESTADO              REINICIOS  ANTIGÜEDAD
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       En ejecución        0          20d
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       En ejecución        0          16d
  es-ibm-es-kafka-sts-0                                 4/4       En ejecución        15         17d
  es-ibm-es-kafka-sts-1                                 4/4       En ejecución        264        15d
  es-ibm-es-kafka-sts-2                                 4/4       En ejecución        370        22d
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       En ejecución        0          9d
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       En ejecución        0          9d
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       En ejecución        0          22d
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       En ejecución        55         16d
  es-ibm-es-zookeeper-sts-0                             1/1       En ejecución        0          17d
  es-ibm-es-zookeeper-sts-1                             1/1       En ejecución        1          15d
  es-ibm-es-zookeeper-sts-2                             1/1       En ejecución        488        9d
  ```

---

## Utilización de la supervisión de {{site.data.keyword.aios_short}}
{: #ts-aiosusemonitor}

### Descripción general
{: #ts-omov}

- En este documento se describe cómo crear un nuevo panel de control para supervisar servicios de {{site.data.keyword.aios_full}}.

### Configuración del panel de control
{: #ts-omsd}

- Obtenga el archivo aios-dashboard.json de ibm-aiopenscale-x86_64-1.0.0.tar.gz.  Este archivo se puede encontrar en el directorio `utils`.
- Inicie sesión en el clúster de ICP `https://${ICP Host}:8443`
- Seleccione `Menú` > `Plataforma` > `Supervisión`
- Pulse el icono `Inicio`
- Pulse el elemento de menú `Importar panel de control`
- Pulse el botón `Cargar archivo .json` y apunte a su aios-dashboard.json
- Seleccione `prometheus` para el campo de entrada prometheus

### Visualización del panel de control
{: #ts-omvd}

El panel de control consta de las filas siguientes:

- Uso total de clúster

  Esta fila muestra el uso de CPU, el uso de memoria y el uso del sistema de archivos de todo el clúster. Los velocímetros muestran si el clúster es
correcto. Si muestran condiciones desfavorables, añada más nodos al clúster o termine los pods no necesarios para dejar espacio para otros despliegues.

- Disponibilidad por servicio

  Esta fila muestra la disponibilidad de cada servicio.  Los paneles iniciales muestran los contenedores totales listos.  Si el velocímetro muestra el
100%, su {{site.data.keyword.aios_short}} es correcto.  De lo contrario, puede buscar en la tabla para averiguar qué servicio está inactivo para
llevar a cabo la acción para poner dicho servicio en funcionamiento.  Hay otros runbooks de {{site.data.keyword.aios_short}} que le ayudan a
diagnosticar por qué un contenedor no se ha iniciado correctamente.  Después de los paneles iniciales se encuentran los paneles de servicios individuales. Diferentes líneas muestran el número de contenedores que están listos
y que se solicitan.

- CPU por servicio

  Esta fila muestra el uso de CPU para cada servicio e incluye el número de núcleos de CPU que utiliza cada contenedor y el número límite de núcleos
de CPU que cada contenedor puede utilizar.  Si estos valores son demasiado cercanos, compruebe por qué el contenedor consume mucho recurso de cpu.  Si es necesario, puede aumentar el límite de CPU para cada contenedor editando el despliegue y actualizar el límite de CPU:
  ```bash
  kubectl -n aiopenscale edit deployment ${nombre de despliegue}
  ```

  Ejemplo:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Memoria por servicio

  Esta fila muestra el uso de memoria para cada servicio e incluye la memoria que utiliza cada contenedor y la memoria que cada contenedor puede
utilizar.  Si estos valores son demasiado cercanos, compruebe por qué el contenedor consume mucha memoria.  Si es necesario, puede aumentar la memoria para ese contenedor editando el despliegue y actualizando el límite de memoria:
  ```bash
  kubectl -n aiopenscale edit deployment ${nombre de despliegue}
  ```

  Ejemplo:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Sistema de archivos por servicio

  Esta fila muestra el uso del sistema de archivos para cada servicio.  Si el monitor muestra que el uso de los sistemas de archivos aumenta
constantemente, inspeccione el contenedor para ver por qué el uso del sistema de archivos sigue aumentando.  Si es necesario, puede ponerse en contacto con
el canal de Slack anterior para obtener más ayuda.

- Imágenes y versiones

  Esta fila lista todas las imágenes y las versiones que se utilizan para {{site.data.keyword.aios_full}}.
