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

# 문제점 해결
{: #ts-trouble}

## {{site.data.keyword.aios_full}}의 공통적인 문제
{: #ts-trouble-common}

다음 문제는 {{site.data.keyword.aios_full}} on Cloud 및 {{site.data.keyword.wos4d_full}} 모두에서 공통적으로 발생합니다.

### 페이로드 분석이 적절하게 표시되지 않음
{: #ts-trouble-common-payloadfileformat}

- 상황: 다음 오류 메시지가 표시됩니다.
  - 오류 코드: AIQDT0044E
  - 오류 텍스트: 열 이름 `<column name>`에 금지 문자 `"`가 있음

- 상황: 페이로드 분석의 적절한 처리를 위해 {{site.data.keyword.aios_short}}에서는 큰따옴표(")가 있는 열 이름을 페이로드에 사용하는 것을 지원하지 않습니다. 이는 CSV 및 JSON 형식의 피드백 데이터 및 스코어링 페이로드에 영향을 미칩니다.
- 솔루션: 페이로드 파일의 열 이름에서 큰따옴표(")를 제거하십시오.

## {{site.data.keyword.wos4d_full}} 관련 문제
{: #ts-trouble-icp}

다음 문제는 {{site.data.keyword.wos4d_full}}에서만 발생합니다.

## 편향성/공정성 서비스가 작동 중지됨
{: #ts-bfdown}

### 개요
{: #ts-bfdov}

- 상황: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-bfdck}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-bfdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    상태가 **실행 중**이며 완전히 준비된 **2/2**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o <format> 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

    - 이미지 이름이 올바른지 확인합니다.
    - 저장소에 이미지를 푸시했습니까?
    - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      이 팟에는 세 개의 컨테이너 aios-bias, ml-gateway-sidecar 및 check-etcd-ready가 있으므로 aios-bias에 문제가 없는 경우 ml-gateway-sidecar 및 check-etcd-ready 로그도 확인해야 합니다.

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---
## {{site.data.keyword.aios_short}} 서비스가 작동 중지됨
{: #ts-aiosdown}

### 개요
{: #ts-odov}

- 상황: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다. . .
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-odkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용

    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-odvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

        팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

        - 클러스터에 노드를 추가합니다.

        - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
        ```bash
      kubectl -n [namespace] delete pod [pod name]
        ```

        - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

        - 이미지 이름이 올바른지 확인합니다.
        - 저장소에 이미지를 푸시했습니까?
        - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---
## {{site.data.keyword.aios_short}} 구성 서비스가 작동 중지됨
{: #ts-aiosconfigdown}

### 개요
{: #ts-ocdov}

- 상황: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-ocdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-ocdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-configuration-554f548667-7l782`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 대시보드 서비스가 작동 중지됨
{: #ts-aiosdashdown}

### 개요
{: #ts-oddov}

- 상황: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: N/A

### kubectl 구성
{: #ts-oddkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-oddvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---
## 데이터 마트 서비스가 작동 중지됨
{: #ts-datamartdown}

### 개요
{: #ts-dmdov}

- 상황: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-dmdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-dmdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## 설명 가능성 서비스가 작동 중지됨
{: #ts-expdown}

### 개요
{: #ts-esdov}

- 상황: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-esdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-esdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    상태가 **실행 중**이며 완전히 준비된 **2/2**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      이 팟에는 세 개의 컨테이너 explainability-service, ml-gateway-sidecar 및 check-etcd-ready가 있으므로 explainability-service에 문제가 없는 경우 ml-gateway-sidecar 및 check-etcd-ready 로그도 확인해야 합니다.

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 피드백 서비스가 작동 중지됨
{: #ts-aiosfeedbackdown}

### 개요
{: #ts-fsdov}

- 상황: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: etcd

### kubectl 구성
{: #ts-fsdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-fsdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **2/2**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      이 팟에는 세 개의 컨테이너 aios-feedback, ml-gateway-sidecar 및 check-etcd-ready가 있으므로 aios-feedback에 문제가 없는 경우 ml-gateway-sidecar 및 check-etcd-ready 로그도 확인해야 합니다.

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 검색 서비스가 작동 중지됨
{: #ts-aiosdiscdown}

### 개요
{: #ts-dsdov}

- 상황: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: N/A

### kubectl 구성
{: #ts-dsdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  옵션 2: {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-dsdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} nginx 서비스가 작동 중지됨
{: #ts-aiosnginxdown}

### 개요
{: #ts-nsdov}

- 상황: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: N/A

### kubectl 구성
{: #ts-nsdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-nsdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 페이로드 로깅 API 서비스가 작동 중지됨
{: #ts-aiospayloadapidown}

### 개요
{: #ts-pladov}

- 상황: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 외부 서비스(Azur, Amazon 등)에서 당사의 서비스에 페이로드를 쓸 수 없으므로 고객이 분석할 현재 데이터가 없습니다.
- 모니터링 시스템:
- 종속 항목: IBM Event Stream

### kubectl 구성
{: #ts-pladkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-pladvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o <format> 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 페이로드 로깅 서비스가 작동 중지됨
{: #ts-aiospayloaddown}

### 개요
{: #ts-plsdov}

- 상황: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 외부 서비스(Azur, Amazon 등)에서 당사의 서비스에 페이로드를 쓸 수 없으므로 고객이 분석할 현재 데이터가 없습니다.
- 모니터링 시스템:
- 종속 항목: IBM Event Stream

### kubectl 구성
{: #ts-plsdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-plsdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8`을 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o <format> 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} 스케줄링 서비스가 작동 중지됨
{: #ts-aiosscheddown}

### 개요
{: #ts-ssdov}

- 상황: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: N/A

### kubectl 구성
{: #ts-ssdkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}`:8443에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-ssdvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## {{site.data.keyword.aios_short}} redis 서비스가 작동 중지됨
{: #ts-aiosredisdown}

### 개요
{: #ts-redov}

- 상황: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: N/A

### kubectl 구성
{: #ts-redkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-redvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

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

    상태가 **실행 중**이며 완전히 준비된 **1/1**인지 확인하십시오.  다음 예에서는 팟으로 `aios-redis-server-6f4c55fd75-nlrr4`를 사용합니다.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o <format> 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## etcd 서비스가 작동 중지됨
{: #ts-etcddown}

### 개요
{: #ts-etcov}

- 상황: etcd_micro_service_is_down:
- 고객에게 미치는 영향: 고객이 새 인스턴스 구성, 요청 분석, 페이로드 저장 등의 기능을 사용할 수 없습니다.
- 모니터링 시스템:
- 종속 항목: 없음

### kubectl 구성
{: #ts-etckc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 확인/복구 단계
{: #ts-etcvr}

1.  다음 명령으로 팟의 상태를 확인하십시오.

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

    etcd 팟이 세 개 있으며 해당 상태가 **실행 중**이고 완전히 준비된 **1/1**인지 확인하십시오.

1.  팟이 실행 중 상태가 아니면 다음과 같이 팟을 설명하십시오.

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    이 명령을 실행하면 팟에 관한 상세 정보가 표시됩니다.  팟이 실행 중 상태가 아니면 오류도 제공합니다.  실행 중 상태가 아니면 팟에서 다음 경우도 발생할 수 있습니다.

    - **내 팟이 계속 보류 중 상태임**

      팟이 계속 **보류 중** 상태에 있으면 노드에서 스케줄링할 수 없다는 의미입니다.  일반적으로 특정 유형의 리소스가 충분하지 않아 스케줄링을 방지하기 때문입니다.  자세한 정보를 얻으려면 이전 명령을 실행하십시오. 스케줄러에서 팟을 스케줄링할 수 없는 이유를 나타내는 메시지를 표시해야 합니다. 클러스터에서 CPU 또는 메모리 공급이 소진되었을 수 있습니다. 이 경우 다음과 같은 여러 조치를 수행할 수 있습니다.

      - 클러스터에 노드를 추가합니다.

      - 불필요한 팟을 종료하여 보류 중인 팟의 공간을 마련합니다.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - 팟이 노드보다 크지 않은지 확인합니다. 예를 들어 모든 노드에 cpu:1의 용량이 있으면 cpu: 1.1 요청이 있는 팟은 스케줄링하지 않습니다.

      kubectl get nodes -o `<format>` 명령을 사용하여 노드 용량을 확인할 수 있습니다. 필수 정보만 추출하는 예제 명령행은 다음과 같습니다.
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **내 팟이 계속 대기 중임**

      팟이 **대기 중** 상태에 머물러 있는 경우 작업자 노드로 스케줄링할 수 있지만 해당 머신에서 실행할 수 없습니다. 마찬가지로 kubectl describe에서 정보를 제공해야 합니다. 팟이 **대기 중**인 가장 일반적인 이유는 이미지를 가져오는 데 실패했기 때문입니다. 이를 확인하는 방법은 다음 세 가지가 있습니다.

      - 이미지 이름이 올바른지 확인합니다.
      - 저장소에 이미지를 푸시했습니까?
      - 이미지를 가져올 수 있는지 확인하기 위해 직접 `docker pull`을 실행하여 클러스터에서 이미지를 가져옵니다.

    - **내 팟이 충돌했거나 상태가 양호하지 않음**

      먼저 현재 컨테이너의 로그를 확인하십시오.
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      이전에 컨테이너가 충돌한 경우 다음을 사용하여 이전 컨테이너의 충돌 로그에 액세스할 수 있습니다.
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      일반적으로 로그에는 팟이 시작되지 않는 이유에 관한 정보가 있어야 합니다.  로그의 정보를 기반으로 문제점을 정정하십시오.  이 접근 방식이 작동하지 않으면 에스컬레이션 단계를 진행하십시오.

---

## event_stream으로 대시보드 작성
{: #ts-createdashes}

### 개요
{: #ts-dshov}

- 이 문서에서는 {{site.data.keyword.aios_full}} 서비스를 모니터링하는 새 대시보드 작성 방법을 설명합니다.

### kubectl 구성
{: #ts-dshkc}

kubectl 클라이언트는 다음 두 가지 방법으로 구성할 수 있습니다.

1.  cloudctl 도구 사용

    랩탑에서 cloudctl을 사용할 수 있으면 다음 명령을 실행하여 kubectl을 구성하십시오.
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    `${username}`,  `${password}`, `${ICP Host}`를 진짜 값으로 대체하십시오.  예를 들어 다음과 같습니다.
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  {{site.data.keyword.icpfull}} 콘솔에서 kubectl 구성 사용
    - {{site.data.keyword.icpfull}} 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
    - **둥근 사용자** 아이콘 > **클라이언트 구성**을 선택하십시오.
    - **클립보드에 복사** 아이콘을 클릭하여 구성 정보를 클립보드에 복사합니다.
    - 필요한 경우 네임스페이스를 `aiopenscale`에서 `es`로 변경합니다.
    - 구성 정보를 명령행에 붙여넣고 **Enter**를 누릅니다.

### 이벤트 스트림 보기
{: #ts-dshve}

이벤트 스트림은 여러 서비스로 구성됩니다.  각 서비스의 상세 정보는 하위 폴더를 참조하십시오.

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

## {{site.data.keyword.aios_short}} 모니터링 사용
{: #ts-aiosusemonitor}

### 개요
{: #ts-omov}

- 이 문서에서는 {{site.data.keyword.aios_full}} 서비스를 모니터링하는 새 대시보드 작성 방법을 설명합니다.

### 대시보드 설정
{: #ts-omsd}

- ibm-aiopenscale-x86_64-1.0.0.tar.gz에서 aios-dashboard.json 파일을 가져오십시오.  이 파일은 `utils` 디렉토리에서 찾을 수 있습니다.
- ICP 클러스터 `https://${ICP Host}:8443`에 로그인합니다.
- `메뉴` > `플랫폼` > `모니터링`을 선택합니다.
- `홈` 아이콘을 클릭합니다.
- `대시보드 가져오기` 메뉴 항목을 클릭합니다.
- `Upload .json 파일` 단추를 클릭하고 aios-dashboard.json을 가리킵니다.
- Prometheus 입력 필드의 경우 `prometheus`를 선택합니다.

### 대시보드 보기
{: #ts-omvd}

대시보드는 다음 행으로 구성됩니다.

- 클러스터 총 사용량

  이 행에서는 클러스터 전체 CPU 사용량, 메모리 사용량 및 파일 시스템 사용량을 보여줍니다. 속도계에서는 클러스터의 상태가 양호한지 보여줍니다. 상태가 양호하지 않다고 표시하면 클러스터에 노드를 추가하거나 불필요한 팟을 종료하여 다른 배치에 사용할 공간을 마련하십시오.

- 서비스별 가용성

  이 행에서는 각 서비스의 가용성을 보여줍니다.  초기 패널에서는 준비된 전체 컨테이너를 보여줍니다.  속도계에 100%가 표시되면 {{site.data.keyword.aios_short}}의 상태가 양호한 것입니다.  그렇지 않으면 테이블에서 작동 중단된 서비스를 확인하여 해당 서비스를 다시 작동시킬 조치를 취할 수 있습니다.  컨테이너가 시작되지 않는 이유를 진단하는 데 사용할 수 있는 다른 {{site.data.keyword.aios_short}} Runbook이 있습니다.  초기 패널 다음에는 개별 서비스의 패널이 옵니다. 준비된 컨테이너 수와 요청된 컨테이너 수는 서로 다른 행에 표시됩니다.

- 서비스별 CPU

  이 행에는 각 서비스의 CPU 사용량이 표시되고 각 컨테이너에서 사용하는 CPU 코어 수와 각 컨테이너에서 사용할 수 있는 CPU 코어의 한계 수가 포함되어 있습니다.  이 값에 너무 가까워지면 컨테이너에서 cpu 리소스를 많이 사용하는 이유를 확인하십시오.  필요한 경우 배치를 편집하여 해당 컨테이너의 cpu 한계를 늘리고 cpu 한계를 업데이트할 수 있습니다.
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  예:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 서비스별 메모리

  이 행에는 각 서비스의 메모리 사용량이 표시되고 각 컨테이너에서 사용하는 메모리와 각 컨테이너에서 사용할 수 있는 메모리가 포함되어 있습니다.  이 값에 너무 가까워지면 컨테이너에서 메모리를 많이 사용하는 이유를 확인하십시오.  필요한 경우 배치를 편집하여 컨테이너의 메모리를 늘리고 메모리 한계를 업데이트할 수 있습니다.
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  예:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- 서비스별 파일 시스템

  이 행에서는 각 서비스의 파일 시스템 사용량을 표시합니다.  모니터에서 파일 시스템 사용량이 지속적으로 증가하는 것을 표시하면 컨테이너에서 파일 시스템 사용량이 계속 증가하는 이유를 확인하십시오.  필요한 경우 이전 Slack 채널에 문의하여 추가 도움을 얻을 수 있습니다.

- 이미지 및 버전

  이 행에서는 {{site.data.keyword.aios_full}}애 사용된 모든 이미지와 버전을 나열합니다.
