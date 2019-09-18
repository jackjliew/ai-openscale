---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"


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

# Troubleshooting
{: #ts-trouble}

## Common issues for {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

The following issues are common for both {{site.data.keyword.aios_full}} on Cloud and {{site.data.keyword.wos4d_full}}.

### Error in running drift with XGBoost model
{: #ts-trouble-common-xgboost-wml-model-details}

The following messages while completing the **Model details** section during configuration indicate an input schema mismatch:

- Field `feature_fields` references column `<name>`, which is missing in `input_schema`
- Feature not found in input schema

To fix the issue, you must determine which of the following conditions is causing the error and take corrective action:

- If you use {{site.data.keyword.pm_full}} as your machine learning provider and the model type is XGBoost/scikit-learn refer to the {{site.data.keyword.pm_short}} [Python SDK documentation](http://wml-api-pyclient-dev.mybluemix.net/#repository) for important information about how to store the model.

- For all other cases, you must ensure that the training data column names match.



### Payload analytics does not display properly
{: #ts-trouble-common-payloadfileformat}

- Situation: The following error message displays:
  - error code: AIQDT0044E
  - error text: Forbidden character `"` in column name `<column name>`

- Situation: For proper processing of payload analytics, {{site.data.keyword.aios_short}} does not support column names with double quotation marks (") in the payload. This affects both scoring payload and feedback data in CSV and JSON formats.
- Solution: Remove double quotation marks (") from the column names of the payload file.

### Active debias records do not reach the payload logging table
{: #ts-trouble-common-payloadlogging-1000k-limit}

Not all debias records reach the payload logging table. There is also a mis-match in the records count in the error log, where you might see the following error message:

`com.ibm.analytics.aios.utils.clients.db.TableSchemaMismatch: Existing table schema does not match with expectation`

When you use the active debias API, there is a limit of 1000 records that can be sent at one time for payload logging.

To avoid loss of data, you must use the active debias API to score in chunks of 1000 records or fewer.

## Issues specific to {{site.data.keyword.wos4d_full}}
{: #ts-trouble-icp}

The following issues are specific to {{site.data.keyword.wos4d_full}}:

## Bias/Fairness service is down
{: #ts-bfdown}

### Overview
{: #ts-bfdov}

- Situation: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-bfdck}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-bfdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    Ensure that the status is **running** and it is fully ready **2/2**.  We will use `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o <format> command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

    - Make sure that you have the name of the image correct.
    - Have you pushed the image to the repository?
    - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Because this pod has 3 containers aios-bias , ml-gateway-sidecar and check-etcd-ready, you should also take a look into the log of ml-gateway-sidecar and check-etcd-ready if aios-bias does not have any problem:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    In general, the logs should contain information why the pod is not started successfully.  Correct the problem based on the information from the logs.  If none of these approaches work, please continue to the Escalation steps

---
## {{site.data.keyword.aios_short}} service is down
{: #ts-aiosdown}

### Overview
{: #ts-odov}

- Situation: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload . . .
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-odkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console

    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-odvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

        If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

        - Add more nodes to the cluster.

        - Terminate unneeded pods to make room for pending pods.
        ```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

        - Make sure that you have the name of the image correct.
        - Have you pushed the image to the repository?
        - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---
## {{site.data.keyword.aios_short}} configuration service is down
{: #ts-aiosconfigdown}

### Overview
{: #ts-ocdov}

- Situation: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-ocdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

If cloudctl is available on your laptop, run the following command to configure kubectl:

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-ocdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-configuration-554f548667-7l782` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} dashboard service is down
{: #ts-aiosdashdown}

### Overview
{: #ts-oddov}

- Situation: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: N/A

### Configure kubectl
{: #ts-oddkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-oddvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---
## Data Mart service is down
{: #ts-datamartdown}

### Overview
{: #ts-dmdov}

- Situation: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-dmdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-dmdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## Explainability service is down
{: #ts-expdown}

### Overview
{: #ts-esdov}

- Situation: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-esdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-esdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    Ensure that the status is **running** and it is fully ready **2/2**.  We will use `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Because this pod has 3 containers explainability-service, ml-gateway-sidecar and check-etcd-ready, you should also take a look into the log of ml-gateway-sidecar and check-etcd-ready if explainability-service does not have any problem:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      In general, the logs should contain information why the pod is not started successfully.  Correct the problem based on the information from the logs.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} feedback service is down
{: #ts-aiosfeedbackdown}

### Overview
{: #ts-fsdov}

- Situation: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: etcd

### Configure kubectl
{: #ts-fsdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-fsdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **2/2**.  We will use `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Because this pod has 3 containers aios-feedback, ml-gateway-sidecar and check-etcd-ready, you should also take a look into the log of ml-gateway-sidecar and check-etcd-ready if aios-feedback does not have any problem:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      In general, the logs should contain information why the pod is not started successfully.  Correct the problem based on the information from the logs.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} discovery service is down
{: #ts-aiosdiscdown}

### Overview
{: #ts-dsdov}

- Situation: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: N/A

### Configure kubectl
{: #ts-dsdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Option 2: Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-dsdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} nginx service is down
{: #ts-aiosnginxdown}

### Overview
{: #ts-nsdov}

- Situation: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: N/A

### Configure kubectl
{: #ts-nsdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-nsdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} payload logging API service is down
{: #ts-aiospayloadapidown}

### Overview
{: #ts-pladov}

- Situation: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Customer Impact: Customers can't write Payload to our service from exteranl services (Azur, Amazon, other) so customers don't have current data for analyze.
- Monitoring System:
- Dependencies: IBM Event Stream

### Configure kubectl
{: #ts-pladkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-pladvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o <format> command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} payload logging service is down
{: #ts-aiospayloaddown}

### Overview
{: #ts-plsdov}

- Situation: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Customer Impact: Customers can't write Payload to our service from external services (Azur, Amazon, other) so customers don't have current data for analyze.
- Monitoring System:
- Dependencies: IBM Event Stream

### Configure kubectl
{: #ts-plsdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-plsdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running    1         6h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o <format> command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} scheduling service is down
{: #ts-aiosscheddown}

### Overview
{: #ts-ssdov}

- Situation: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: N/A

### Configure kubectl
{: #ts-ssdkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}`:8443
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-ssdvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## {{site.data.keyword.aios_short}} redis service is down
{: #ts-aiosredisdown}

### Overview
{: #ts-redov}

- Situation: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: N/A

### Configure kubectl
{: #ts-redkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-redvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    aios-redis-sentinel-6d5bffbcd8-hjvgk                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-j4htd                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-w4vcb                          1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-h4nfh                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-k9ggw                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-nlrr4                            1/1       Running    0          14m
    ```

    Ensure that the status is **running** and it is fully ready **1/1**.  We will use `aios-redis-server-6f4c55fd75-nlrr4` as our pod for the following examples.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o <format> command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## etcd service is down
{: #ts-etcddown}

### Overview
{: #ts-etcov}

- Situation: etcd_micro_service_is_down:
- Customer Impact: Customers can't use any functionality such as configure new instances, analyze of requests, store payload ...
- Monitoring System:
- Dependencies: None

### Configure kubectl
{: #ts-etckc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Paste the configuration information to your command line, and press **Enter**.

### Verification/Recovery steps
{: #ts-etcvr}

1.  Check pod's status with the following commands:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    NAME                                         READY     STATUS    RESTARTS   AGE
    etcd-0                                       1/1       Running             3          8d
    etcd-1                                       1/1       Running             0          8d
    etcd-2                                       1/1       Running             0          8d
    ```

    Ensure that there are three etcd pods, their status are **running**, and they are fully ready **1/1**.

1.  Describe the pod if the pod is not in running stage:

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    This command will display details about the pod.  This also provides errors if your pod is not in running stage.  Your pod might encounter the following cases when it is not running stage:

    - **My pod stays pending**

      If the pod stays **Pending**, it means that it can not be scheduled onto a node.  Generally this is because there are insufficient resource of one type or another that prevent scheduling.  Run the preceding command to get more information. There should be messages from the scheduler about why it can not schedule your pod. You may have exhausted the supply of CPU or Memory in your cluster. In this case you can try several things:

      - Add more nodes to the cluster.

      - Terminate unneeded pods to make room for pending pods.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Check that the pod is not larger than your nodes. For example, if all nodes have a capacity of cpu:1, then a pod with a request of cpu: 1.1 will never be scheduled.

      You can check node capacities with the kubectl get nodes -o `<format>` command. Here are some example command lines that extract just the necessary information:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **My pod stays waiting**

      If a pod is stuck in the **Waiting** state, then it has been scheduled to a worker node, but it can’t run on that machine. Again, the information from kubectl describe ... should be informative. The most common cause of **Waiting** pods is a failure to pull the image. There are three things to check:

      - Make sure that you have the name of the image correct.
      - Have you pushed the image to the repository?
      - Run a manual `docker pull` to pull the image on your cluster to see if the image can be pulled.

    - **My pod is crashing or otherwise unhealthy**

      First, take a look at the logs of the current container:
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      If your container has previously crashed, you can access the previous container’s crash log with:
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      In general, the log should contain information why the pod is not started successfully.  Correct the problem based on the information from the log.  If none of these approaches work, please continue to the Escalation steps

---

## Create a dashboard with event_stream
{: #ts-createdashes}

### Overview
{: #ts-dshov}

- This document describe how to create new dashboard to monitor {{site.data.keyword.aios_full}} services.

### Configure kubectl
{: #ts-dshkc}

There are two ways to configure kubectl client.

1.  Using cloudctl tool

    If cloudctl is available on your laptop, run the following command to configure kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    Replace `${username}`,  `${password}`, `${ICP Host}` with true value.  For example:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Using kubectl configuration from {{site.data.keyword.icpfull}} console
    - Log in to your {{site.data.keyword.icpfull}} cluster `https://${ICP Host}:8443`
    - Select the **round person** icon > **Configure client**
    - Click on **Copy to clipboard** icon to copy the configuration information to clipboard
    - Change namespace from `aiopenscale` to `es` if needed.
    - Paste the configuration information to your command line, and press **Enter**.

### Viewing event stream
{: #ts-dshve}

The event stream consists of several services.  Please see subfolder for details of each service.

  ```bash
  $ kubectl get pods -n eventstream
  NAME                                                  READY     STATUS              RESTARTS   AGE
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       Running               0        20d
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       Running               0        16d
  es-ibm-es-kafka-sts-0                                 4/4       Running              15        17d
  es-ibm-es-kafka-sts-1                                 4/4       Running             264        15d
  es-ibm-es-kafka-sts-2                                 4/4       Running             370        22d
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       Running               0         9d
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       Running               0         9d
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       Running               0        22d
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       Running              55        16d
  es-ibm-es-zookeeper-sts-0                             1/1       Running               0        17d
  es-ibm-es-zookeeper-sts-1                             1/1       Running               1        15d
  es-ibm-es-zookeeper-sts-2                             1/1       Running             488         9d
  ```

---

## Using {{site.data.keyword.aios_short}} monitoring
{: #ts-aiosusemonitor}

### Overview
{: #ts-omov}

- This document describe how to create new dashboard to monitor {{site.data.keyword.aios_full}} services.

### Setting up the dashboard
{: #ts-omsd}

- Get aios-dashboard.json file from ibm-aiopenscale-x86_64-1.0.0.tar.gz.  This file can be found from `utils` directory.
- Log in to your ICP cluster `https://${ICP Host}:8443`
- Select `Menu` > `Platform` > `Monitoring`
- Click `Home` icon
- Click `Import dashboard` menu item
- Click `Upload .json File` button and point to your aios-dashboard.json
- Select `prometheus` for prometheus input field

### Viewing the dashboard
{: #ts-omvd}

The dashboard consists of the following rows:

- Cluster total usage

  This row shows cluster-wide CPU usage, memory usage, and filesystem usage. The speedometers show whether you cluster is healthy. If they show unhealthy conditions, add more nodes to the cluster or terminate unneeded pods to make room for other deployments.

- Availability by service

  This row shows availability for each service.  The initial panels shows total containers ready.  If the speedometer shows 100%, then your {{site.data.keyword.aios_short}} is healthy.  Otherwise, you can look into the table to find out what service is down to take action to bring that service up.  There are other {{site.data.keyword.aios_short}} runbooks that help to diagnostic why a container is not started successfully.  Following the initial panels are the panels for individual services. Different lines show the number of containers that are ready and that are requested.

- CPU by service

  This row shows CPU usage for each service and includes the number of CPU cores that each container uses and the limit number of CPU cores that each container can use.  If these values are too close, check why the container consumes to much cpu resource.  If needed, you can increase the limit of cpu for that container by editing deployment and update litmit of cpu:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Example:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Memory by service

  This row shows memory usage for each service and includes the memory that each container uses and the memory that each container can use.  If these values are too close, check why the container consumes to much memory.  If needed, you can increase memory for that container by editing the deployment and update limit of memory:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Example:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Filesystem by service

  This row shows filesystem usage for each service.  If the monitor shows filesytem usage constantly increasing, inspect the container to see why filesystem usage keeps going up.  If needed, you can contact the preceding Slack channel for further help.

- Images and versions

  This row lists all images and versions that are used for {{site.data.keyword.aios_full}}.
