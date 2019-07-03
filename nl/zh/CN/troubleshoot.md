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

# 故障诊断
{: #ts-trouble}

## {{site.data.keyword.aios_full}} 的常见问题
{: #ts-trouble-common}

以下问题对于 {{site.data.keyword.aios_full}} on Cloud 和 {{site.data.keyword.wos4d_full}} 均很常见。

### 有效内容分析未正确显示
{: #ts-trouble-common-payloadfileformat}

- 情境：显示以下错误消息：
  - 错误代码：AQDT0044E
  - 错误文本：在列名 `<column name>` 中出现禁止的字符 `"`

- 情境：为正确处理有效内容分析，{{site.data.keyword.aios_short}} 不支持在有效内容中使用带有双引号 (") 的列名。这将影响 CSV 和 JSON 格式的评分有效内容和反馈数据。
- 解决方案：从有效内容文件的列名中移除双引号 (")。

## 特定于 {{site.data.keyword.wos4d_full}} 的问题
{: #ts-trouble-icp}

以下问题特定于 {{site.data.keyword.wos4d_full}}：

## 偏差/公平性服务已关闭
{: #ts-bfdown}

### 概述
{: #ts-bfdov}

- 情境：ai-open-scale-ibm-aios-bias_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-bfdck}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-bfdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    确保状态为 **Running** 并完全就绪 **2/2**。对于以下示例，将使用 `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o <format> 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

    - 确保映像名称正确。
    - 是否已将映像推送到存储库？
    - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      由于此 pod 具有 3 个容器（aios-bias、ml-gateway-sidecar 和 check-etcd-ready），因此如果 aios-bias 没有任何问题，那么还应查看 ml-gateway-sidecar 和 check-etcd-ready 的日志：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---
## {{site.data.keyword.aios_short}} 服务已关闭
{: #ts-aiosdown}

### 概述
{: #ts-odov}

- 情境：ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-odkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置

    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-odvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

        如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

        - 向集群添加更多节点。

        - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

        - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

        - 确保映像名称正确。
        - 是否已将映像推送到存储库？
        - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---
## {{site.data.keyword.aios_short}} 配置服务已关闭
{: #ts-aiosconfigdown}

### 概述
{: #ts-ocdov}

- 情境：ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-ocdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-ocdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-configuration-554f548667-7l782` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 仪表板服务已关闭
{: #ts-aiosdashdown}

### 概述
{: #ts-oddov}

- 情境：ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：不适用

### 配置 kubectl
{: #ts-oddkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-oddvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---
## 数据集市服务已关闭
{: #ts-datamartdown}

### 概述
{: #ts-dmdov}

- 情境：ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-dmdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-dmdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## 可解释性服务已关闭
{: #ts-expdown}

### 概述
{: #ts-esdov}

- 情境：ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-esdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-esdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    确保状态为 **Running** 并完全就绪 **2/2**。对于以下示例，将使用 `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      由于此 pod 具有 3 个容器（explainability-service、ml-gateway-sidecar 和 check-etcd-ready），因此如果 explainability-service 没有任何问题，那么还应查看 ml-gateway-sidecar 和 check-etcd-ready 的日志：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 反馈服务已关闭
{: #ts-aiosfeedbackdown}

### 概述
{: #ts-fsdov}

- 情境：ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：etcd

### 配置 kubectl
{: #ts-fsdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-fsdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running   1          6h
    ```

    确保状态为 **Running** 并完全就绪 **2/2**。对于以下示例，将使用 `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      由于此 pod 具有 3 个容器（aios-feedback、ml-gateway-sidecar 和 check-etcd-ready），因此如果 aios-feedback 没有任何问题，那么还应查看 ml-gateway-sidecar 和 check-etcd-ready 的日志：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 发现服务已关闭
{: #ts-aiosdiscdown}

### 概述
{: #ts-dsdov}

- 情境：ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：不适用

### 配置 kubectl
{: #ts-dsdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  选项 2：从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-dsdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} nginx 服务已关闭
{: #ts-aiosnginxdown}

### 概述
{: #ts-nsdov}

- 情境：ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：不适用

### 配置 kubectl
{: #ts-nsdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-nsdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 有效内容日志记录 API 服务已关闭
{: #ts-aiospayloadapidown}

### 概述
{: #ts-pladov}

- 情境：ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- 客户影响：客户无法将有效内容从外部服务（Azur、Amazon 和其他）写入到我们的服务，因此客户没有供分析的当前数据。
- 监视系统：
- 依赖关系：IBM Event Stream

### 配置 kubectl
{: #ts-pladkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-pladvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o <format> 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 有效内容日志记录服务已关闭
{: #ts-aiospayloaddown}

### 概述
{: #ts-plsdov}

- 情境：ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- 客户影响：客户无法将有效内容从外部服务（Azur、Amazon 和其他）写入到我们的服务，因此客户没有供分析的当前数据。
- 监视系统：
- 依赖关系：IBM Event Stream

### 配置 kubectl
{: #ts-plsdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-plsdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running   1          6h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o <format> 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} 调度服务已关闭
{: #ts-aiosscheddown}

### 概述
{: #ts-ssdov}

- 情境：ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：不适用

### 配置 kubectl
{: #ts-ssdkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}`:8443
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-ssdvr}

1.  使用以下命令检查 pod 的状态：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## {{site.data.keyword.aios_short}} redis 服务已关闭
{: #ts-aiosredisdown}

### 概述
{: #ts-redov}

- 情境：ai-open-scale-ibm-aios-redis_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：不适用

### 配置 kubectl
{: #ts-redkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-redvr}

1.  使用以下命令检查 pod 的状态：

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

    确保状态为 **Running**，并且该 pod 完全就绪 **1/1**。对于以下示例，将使用 `aios-redis-server-6f4c55fd75-nlrr4` 作为 pod。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o <format> 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## etcd 服务已关闭
{: #ts-etcddown}

### 概述
{: #ts-etcov}

- 情境：etcd_micro_service_is_down:
- 客户影响：客户无法使用任何功能，例如配置新实例，分析请求，存储有效内容...
- 监视系统：
- 依赖关系：无

### 配置 kubectl
{: #ts-etckc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 验证/恢复步骤
{: #ts-etcvr}

1.  使用以下命令检查 pod 的状态：

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

    确保有三个 etcd pod，其状态为 **Running**，并且这些 pod 完全就绪 **1/1**。

1.  如果 pod 未处于运行阶段，请描述该 pod：

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    此命令将显示有关 pod 的详细信息。如果 pod 未处于运行阶段，那么此命令还会提供错误。当 pod 未处于运行阶段时可能会遇到以下情况：

    - **pod 保持暂挂**

      如果 pod 保持 **Pending** 状态，那么意味着无法将其调度到节点上。通常，这是因为某种类型的资源不足，导致无法进行调度。运行以上命令以获取更多信息。调度程序应显示有关无法调度 pod 的原因的消息。您可能已耗尽集群中的 CPU 或内存供应。在此情况下，可以尝试以下几种操作：

      - 向集群添加更多节点。

      - 终止不需要的 pod，以便为暂挂 pod 腾出空间。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 检查 pod 是否大小不超过您的节点。例如，如果所有节点的容量都为 cpu:1，那么将永远不会调度带有 cpu:1.1 请求的 pod。

      可以使用 kubectl get nodes -o `<format>` 命令来检查节点容量。以下是一些仅抽取必要信息的示例命令行：
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **pod 保持等待**

      如果 pod 陷入 **Waiting** 状态，那么表示它已调度到工作程序节点，但无法在该机器上运行。同样，来自 kubectl describe ... 的信息应该很有用。pod 处于 **Waiting** 状态的最常见原因是未能提取映像。需要检查以下三种情况：

      - 确保映像名称正确。
      - 是否已将映像推送到存储库？
      - 运行手动 `docker pull` 来提取集群上的映像，以查看是否可以提取该映像。

    - **pod 发生崩溃或在其他方面运行状况不正常**

      首先，查看当前容器的日志：
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      如果容器先前崩溃过，那么可以使用以下命令来访问先前容器的崩溃日志：
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      通常，日志应包含有关 pod 未成功启动的原因的信息。根据日志中的信息来更正问题。如果这些方法都不适用，请继续执行上报步骤

---

## 使用 event_stream 创建仪表板
{: #ts-createdashes}

### 概述
{: #ts-dshov}

- 本文档描述如何创建新仪表板以监视 {{site.data.keyword.aios_full}} 服务。

### 配置 kubectl
{: #ts-dshkc}

配置 kubectl 客户机有两种方式。

1.  使用 cloudctl 工具

    如果 cloudctl 在笔记本电脑上可用，请运行以下命令来配置 kubectl：
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    将 `${username}`、`${password}`、`${ICP Host}` 替换为真实的值。例如：
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  从 {{site.data.keyword.icpfull}} 控制台使用 kubectl 配置
    - 登录到 {{site.data.keyword.icpfull}} 集群 `https://${ICP Host}:8443`
    - 选择**圆形人物**图标 > **配置客户机**
    - 单击**复制到剪贴板**图标以将配置信息复制到剪贴板
    - 如果需要，请将名称空间从 `aiopenscale` 更改为 `es`。
    - 将配置信息粘贴到命令行，然后按 **Enter** 键。

### 查看事件流
{: #ts-dshve}

事件流由多个服务组成。请查看子文件夹以获取每个服务的详细信息。

  ```bash
  $ kubectl get pods -n eventstream
  NAME                                                  READY     STATUS              RESTARTS   AGE
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       Running             0          20d
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       Running             0          16d
  es-ibm-es-kafka-sts-0                                 4/4       Running             15         17d
  es-ibm-es-kafka-sts-1                                 4/4       Running             264        15d
  es-ibm-es-kafka-sts-2                                 4/4       Running             370        22d
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       Running             0          9d
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       Running             0          9d
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       Running             0          22d
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       Running             55         16d
  es-ibm-es-zookeeper-sts-0                             1/1       Running             0          17d
  es-ibm-es-zookeeper-sts-1                             1/1       Running             1          15d
  es-ibm-es-zookeeper-sts-2                             1/1       Running   488        9d
  ```

---

## 使用 {{site.data.keyword.aios_short}} 监视
{: #ts-aiosusemonitor}

### 概述
{: #ts-omov}

- 本文档描述如何创建新仪表板以监视 {{site.data.keyword.aios_full}} 服务。

### 设置仪表板
{: #ts-omsd}

- 从 ibm-aiopenscale-x86_64-1.0.0.tar.gz 获取 aios-dashboard.json 文件。可从 `utils` 目录中找到此文件。
- 登录到 ICP 集群 `https://${ICP Host}:8443`
- 选择`菜单` > `平台` > `监视`
- 单击`主页`图标
- 单击`导入仪表板`菜单项
- 单击`上载 .json 文件`按钮并指向 aios-dashboard.json
- 为 prometheus 输入字段选择 `prometheus`

### 查看仪表板
{: #ts-omvd}

仪表板包含以下行：

- 集群总使用率

  此行显示集群范围的 CPU 使用率、内存使用率和文件系统使用率。里程表显示集群运行状况是否正常。如果它们显示不正常状况，请向集群添加更多节点，或者终止不需要的 pod 来为其他部署腾出空间。

- 按服务划分的可用性

  此行显示每个服务的可用性。初始面板显示就绪的容器总数。如果里程表显示 100%，那么表示 {{site.data.keyword.aios_short}} 运行状况正常。否则，可以查看表来了解哪个服务已关闭，从而采取操作以恢复运行该服务。此外，还有其他有助于诊断容器未成功启动的原因的 {{site.data.keyword.aios_short}} 运行手册。初始面板的下方是个别服务的面板。不同的行显示已就绪和已请求的容器数。

- 按服务划分的 CPU

  此行显示每个服务的 CPU 使用率，并包括每个容器使用的 CPU 核心数以及每个容器可使用的 CPU 核心数限制。如果这些值太接近峰值，请检查容器消耗过多 CPU 资源的原因。如果需要，可以通过编辑部署和更新 CPU 限制来增大该容器的 CPU 限制：
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  示例：
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 按服务划分的内存

  此行显示每个服务的内存使用率，并包括每个容器使用的内存以及每个容器可使用的内存。如果这些值太接近峰值，请检查容器消耗过多内存的原因。如果需要，可以通过编辑部署和更新内存限制来增大容器的内存：
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  示例：
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 按服务划分的文件系统

  此行显示每个服务的文件系统使用率。如果监视器显示文件系统使用率不断增加，请检查容器以了解文件系统使用率保持上升的原因。如果需要，可以联系上面的 Slack 通道以获取进一步帮助。

- 映像和版本

  此行列出用于 {{site.data.keyword.aios_full}} 的所有映像和版本。
