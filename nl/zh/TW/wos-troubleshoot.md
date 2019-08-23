---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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

# 疑難排解
{: #ts-trouble}

## {{site.data.keyword.aios_full}} 共通問題
{: #ts-trouble-common}

以下是 {{site.data.keyword.aios_full}} on Cloud 和 {{site.data.keyword.wos4d_full}} 兩者的共通問題。

### 未適當顯示有效負載分析
{: #ts-trouble-common-payloadfileformat}

- 狀況：顯示下列錯誤訊息：
  - 錯誤碼：AIQDT0044E
  - 錯誤文字：禁用字元 `"` 出現在直欄名稱 `<column name>` 中

- 狀況：為了適當處理有效負載分析，{{site.data.keyword.aios_short}} 不支援帶有雙引號 (") 的直欄名稱出現在有效負載中。這會同時影響 CSV 和 JSON 格式的評分有效負載和回饋資料。
- 解決方案：請將雙引號 (") 從有效負載檔案的直欄名稱中移除。

## {{site.data.keyword.wos4d_full}} 特定的問題
{: #ts-trouble-icp}

以下是 {{site.data.keyword.wos4d_full}} 特定的問題：

## 偏誤/公平性服務已關閉
{: #ts-bfdown}

### 概觀
{: #ts-bfdov}

- 狀況：ai-open-scale-ibm-aios-bias_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-bfdck}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-bfdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    請確定狀態是**執行中**，並已完全備妥 **2/2**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o <format> 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

    - 請確定您的映像檔名稱正確。
    - 您已將映像檔推送至儲存庫？
    - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      由於這個 Pod 有 3 個儲存器，分別是 aios-bias、ml-gateway-sidecar 和 check-etcd-ready，如果 aios-bias 沒有任何問題，您也應查看 ml-gateway-sidecar 和 check-etcd-ready 的日誌：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---
## {{site.data.keyword.aios_short}} 服務已關閉
{: #ts-aiosdown}

### 概觀
{: #ts-odov}

- 狀況：ai-open-scale-ibm-aios-common-api_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、對要求進行分析、儲存有效負載。. .
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-odkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置

    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-odvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

        如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

        - 新增更多節點至叢集。

        - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

        - 請確定您的映像檔名稱正確。
        - 您已將映像檔推送至儲存庫？
        - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---
## {{site.data.keyword.aios_short}} 配置服務已關閉
{: #ts-aiosconfigdown}

### 概觀
{: #ts-ocdov}

- 狀況：ai-open-scale-ibm-aios-configuration_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-ocdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-ocdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-configuration-554f548667-7l782` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 儀表板服務已關閉
{: #ts-aiosdashdown}

### 概觀
{: #ts-oddov}

- 狀況：ai-open-scale-ibm-aios-dashboard_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：N/A

### 配置 kubectl
{: #ts-oddkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-oddvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---
## 「資料集區」服務已關閉
{: #ts-datamartdown}

### 概觀
{: #ts-dmdov}

- 狀況：ai-open-scale-ibm-aios-data-mart_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-dmdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-dmdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## 「可解釋性」服務已關閉
{: #ts-expdown}

### 概觀
{: #ts-esdov}

- 狀況：ai-open-scale-ibm-aios-explainability_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-esdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-esdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    請確定狀態是**執行中**，並已完全備妥 **2/2**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      由於這個 Pod 有 3 個儲存器，分別是 explainability-service、ml-gateway-sidecar 和 check-etcd-ready，如果 explainability-service 沒有任何問題，您也應查看 ml-gateway-sidecar 和 check-etcd-ready 的日誌：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 回饋服務已關閉
{: #ts-aiosfeedbackdown}

### 概觀
{: #ts-fsdov}

- 狀況：ai-open-scale-ibm-aios-feedback_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：etcd

### 配置 kubectl
{: #ts-fsdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-fsdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **2/2**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      由於這個 Pod 有 3 個儲存器，分別是 aios-feedback、ml-gateway-sidecar 和 check-etcd-ready，如果 aios-feedback 沒有任何問題，您也應查看 ml-gateway-sidecar 和 check-etcd-ready 的日誌：

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 探索服務已關閉
{: #ts-aiosdiscdown}

### 概觀
{: #ts-dsdov}

- 狀況：ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：N/A

### 配置 kubectl
{: #ts-dsdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  選項 2：從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-dsdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} nginx 服務已關閉
{: #ts-aiosnginxdown}

### 概觀
{: #ts-nsdov}

- 狀況：ai-open-scale-ibm-aios-nginx_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：N/A

### 配置 kubectl
{: #ts-nsdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-nsdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 有效負載記載 API 服務已關閉
{: #ts-aiospayloadapidown}

### 概觀
{: #ts-pladov}

- 狀況：ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down：
- 客戶影響：客戶無法從外部服務（Azur、Amazon、其他），將「有效負載」寫入至我們的服務，因此客戶沒有現行資料可分析。
- 監視系統：
- 相依關係：IBM Event Stream

### 配置 kubectl
{: #ts-pladkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-pladvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o <format> 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 有效負載記載服務已關閉
{: #ts-aiospayloaddown}

### 概觀
{: #ts-plsdov}

- 狀況：ai-open-scale-ibm-aios-payload-logging_micro_service_is_down：
- 客戶影響：客戶無法從外部服務（Azur、Amazon、其他），將「有效負載」寫入至我們的服務，因此客戶沒有現行資料可分析。
- 監視系統：
- 相依關係：IBM Event Stream

### 配置 kubectl
{: #ts-plsdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-plsdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o <format> 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} 排程服務已關閉
{: #ts-aiosscheddown}

### 概觀
{: #ts-ssdov}

- 狀況：ai-open-scale-ibm-aios-scheduling_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：N/A

### 配置 kubectl
{: #ts-ssdkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}`:8443
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-ssdvr}

1.  使用下列指令來檢查 Pod 的狀態：

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## {{site.data.keyword.aios_short}} redis 服務已關閉
{: #ts-aiosredisdown}

### 概觀
{: #ts-redov}

- 狀況：ai-open-scale-ibm-aios-redis_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：N/A

### 配置 kubectl
{: #ts-redkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-redvr}

1.  使用下列指令來檢查 Pod 的狀態：

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

    請確定狀態是**執行中**，並已完全備妥 **1/1**。在下列範例中，我們將使用 `aios-redis-server-6f4c55fd75-nlrr4` 作為 Pod。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o <format> 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## etcd 服務已關閉
{: #ts-etcddown}

### 概觀
{: #ts-etcov}

- 狀況：etcd_micro_service_is_down：
- 客戶影響：客戶無法使用任何功能，例如：配置新實例、要求的分析、儲存有效負載...
- 監視系統：
- 相依關係：無

### 配置 kubectl
{: #ts-etckc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 驗證/回復步驟
{: #ts-etcvr}

1.  使用下列指令來檢查 Pod 的狀態：

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

    請確定有 3 個 etcd Pod，其狀態是**執行中**，且都已完全備妥 **1/1**。

1.  如果 Pod 不在執行中階段，請說明 Pod：

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    這個指令會顯示 Pod 的詳細資料。如果您的 Pod 不在執行中階段，也會提供錯誤。當您的 Pod 不在「執行中」階段時，它可能遇到下列的情況：

    - **我的 Pod 維持擱置狀態**

      如果 Pod 維持**擱置**，表示無法將它排程到節點。一般而言，這是因為其中一種（或另一種）類型的資源不足，而妨礙其排程。請執行上述指令，以取得其他相關資訊。排程器可能發出訊息，指出無法排程您 Pod 的原因。您可能已耗盡叢集中的 CPU 或記憶體供應量。在此情況下，您可以嘗試下列事項：

      - 新增更多節點至叢集。

      - 終止不必要的 Pod，以騰出空間給擱置的 Pod。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 檢查確定 Pod 沒有大於您的節點。例如，如果所有節點的容量是 cpu:1，當 Pod 的要求是 cpu: 1.1 時，就絕不會排程它。

      您可以使用 kubectl get nodes -o `<format>` 指令，來檢查節點容量。以下的範例指令行只擷取必要的資訊：
```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **我的 Pod 維持等待狀態**

      如果 Pod 停滯在**等待**狀態，表示已將它排程到工作者節點，但是無法在該機器上執行。同樣地，「來自 kubectl 的資訊說明 ...」應該是參考資訊。造成 Pod 處於**等待中**，最常見的原因是無法取回映像檔。有三件事項需要檢查：

      - 請確定您的映像檔名稱正確。
      - 您已將映像檔推送至儲存庫？
      - 執行手動 `docker pull`，取回叢集上的映像檔，看看映像檔能否取回。

    - **我的 Pod 損毀或不健全**

      首先，請查看現行儲存器的日誌：
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      如果您的儲存器先前曾損毀，您可以使用下列指令，存取先前儲存器的損毀日誌：
```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      一般而言，日誌中的資訊應包括指出 Pod 未能順利啟動的原因。請根據日誌中的資訊，來更正問題。如果這些方法都沒有效，請繼續進行「呈報」步驟。

---

## 使用 event_stream 來建立儀表板
{: #ts-createdashes}

### 概觀
{: #ts-dshov}

- 本文件說明如何建立新的儀表板，以監視 {{site.data.keyword.aios_full}} 服務。

### 配置 kubectl
{: #ts-dshkc}

配置 kubectl 用戶端的作法有兩種。

1.  使用 cloudctl 工具

    如果在您的筆記型電腦上可用使用 cloudctl，請執行下列指令來配置 kubectl：
```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    將 `${username}`、`${password}`、`${ICP Host}` 取代為 true 值。例如：
```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  從 {{site.data.keyword.icpfull}} 主控台使用 kubectl 配置
    - 登入您的 {{site.data.keyword.icpfull}} 叢集 `https://${ICP Host}:8443`
    - 選取**萬事通**圖示 > **配置用戶端**
    - 按一下**複製到剪貼簿**圖示，將配置資訊複製到剪貼簿
    - 必要的話，請將名稱空間從 `aiopenscale` 變更為 `es`。
    - 將配置資訊貼到指令行，並按 **Enter** 鍵。

### 檢視事件串流
{: #ts-dshve}

事件串流由數項服務組成。請查看子資料夾，取得每一項服務的詳細資料。

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
  es-ibm-es-zookeeper-sts-1                             1/1       Running            ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         15d
  es-ibm-es-zookeeper-sts-2                             1/1       Running   488        9d
  ```

---

## 使用 {{site.data.keyword.aios_short}} 監視
{: #ts-aiosusemonitor}

### 概觀
{: #ts-omov}

- 本文件說明如何建立新的儀表板，以監視 {{site.data.keyword.aios_full}} 服務。

### 設置儀表板
{: #ts-omsd}

- 從 ibm-aiopenscale-x86_64-1.0.0.tar.gz 取得 aios-dashboard.json 檔。可以從 `utils` 目錄找到這個檔案。
- 登入您的 ICP 叢集 `https://${ICP Host}:8443`
- 選取`功能表` > `平台` > `監視`
- 按一下`首頁`圖示
- 按一下`匯入儀表板`功能表項目
- 按一下`上傳 .json 檔`按鈕，以指向您的 aios-dashboard.json
- 請為 prometheus 輸入欄位，選取 `prometheus`

### 檢視儀表板
{: #ts-omvd}

儀表板由以下各列組成：

- 叢集用量總計

  此列顯示叢集層面的 CPU 使用率、記憶體用量和檔案系統用量。計速器會顯示您的叢集是否性能良好。如果顯示的是性能不佳的狀況，請新增更多節點至叢集，或是終止不必要的 Pod，以騰出空間給其他部署。

- 各服務的可用性

  此列顯示每一項服務的可用性。起始畫面顯示備妥的儲存器總數。如果計速器顯示 100%，表示您的 {{site.data.keyword.aios_short}} 是性能良好的。否則，您可以查看表格，瞭解哪一項服務已關閉，以便採取動作讓該服務啟動。另有其他 {{site.data.keyword.aios_short}} Runbook，可協助您診斷儲存器未能順利啟動的原因。起始畫面之後是個別服務的畫面。不同的線條分別顯示已備妥和所要求的儲存器數目。

- 各服務的 CPU

  此列顯示每一項服務的 CPU 使用率，並且含有每一個儲存器使用的 CPU 核心數目，以及每一個儲存器所能使用的 CPU 核心限制數目。如果這些值太接近，請檢查儲存器為何會耗用過多的 CPU 資源。必要的話，您可以編輯部署來增加該儲存器的 CPU 限制，並更新 CPU 的限制：
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  範例：
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 各服務的記憶體

  此列顯示每一項服務的記憶體用量，並且含有每一個儲存器使用的記憶體，以及每一個儲存器所能使用的記憶體。如果這些值太接近，請檢查儲存器為何會耗用過多的記憶體。必要的話，您可以編輯部署來增加該儲存器的記憶體，並更新記憶體的限制：
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  範例：
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 各服務的檔案系統

  此列顯示每一項服務的檔案系統。如果監視器顯示檔案系統用量不斷增加，請檢查儲存器，瞭解檔案系統用量攀升的原因。必要的話，您可以聯絡上述的 Slack 頻道，取得進一步協助。

- 映像檔和版本

  此列列出用於 {{site.data.keyword.aios_full}} 的所有映像檔和版本。
