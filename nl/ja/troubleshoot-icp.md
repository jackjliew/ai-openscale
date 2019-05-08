---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# トラブルシューティング
{: #ts-trouble}

## バイアス/公平性サービスがダウンした
{: #ts-bfdown}

### 概説
{: #ts-bfdov}

- 状態: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-bfdck}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-bfdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

    - イメージの名前が正しいかどうか。
    - イメージをリポジトリーにプッシュしたかどうか。
    - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      このポッドには、aios-bias、ml-gateway-sidecar、check-etcd-ready という 3 つのコンテナーがあるので、aios-bias に問題がない場合は、ml-gateway-sidecar と check-etcd-ready のログも調べてみる必要があります。

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## {{site.data.keyword.aios_short}} サービスがダウンした
{: #ts-aiosdown}

### 概説
{: #ts-odov}

- 状態: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-odkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する

    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-odvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

        ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

        - クラスターにさらにノードを追加します。

        - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

        - イメージの名前が正しいかどうか。
        - イメージをリポジトリーにプッシュしたかどうか。
        - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## {{site.data.keyword.aios_short}} 構成サービスがダウンした
{: #ts-aiosconfigdown}

### 概説
{: #ts-ocdov}

- 状態: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-ocdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-ocdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-configuration-554f548667-7l782` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ダッシュボード・サービスがダウンした
{: #ts-aiosdashdown}

### 概説
{: #ts-oddov}

- 状態: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: N/A

### kubectl の構成
{: #ts-oddkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-oddvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## データマート・サービスがダウンした
{: #ts-datamartdown}

### 概説
{: #ts-dmdov}

- 状態: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-dmdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-dmdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## 説明可能性サービスがダウンした
{: #ts-expdown}

### 概説
{: #ts-esdov}

- 状態: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-esdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-esdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      このポッドには、explainability-service、ml-gateway-sidecar、check-etcd-ready という 3 つのコンテナーがあるので、explainability-service に問題がない場合は、ml-gateway-sidecar と check-etcd-ready のログも調べてみる必要があります。

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} フィードバック・サービスがダウンした
{: #ts-aiosfeedbackdown}

### 概説
{: #ts-fsdov}

- 状態: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: etcd

### kubectl の構成
{: #ts-fsdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-fsdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      このポッドには、aios-feedback、ml-gateway-sidecar、check-etcd-ready という 3 つのコンテナーがあるので、aios-feedback に問題がない場合は、ml-gateway-sidecar と check-etcd-ready のログも調べてみる必要があります。

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ディスカバリー・サービスがダウンした
{: #ts-aiosdiscdown}

### 概説
{: #ts-dsdov}

- 状態: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: N/A

### kubectl の構成
{: #ts-dsdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  オプション 2: IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-dsdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} nginx サービスがダウンした
{: #ts-aiosnginxdown}

### 概説
{: #ts-nsdov}

- 状態: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: N/A

### kubectl の構成
{: #ts-nsdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-nsdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ペイロード・ロギング API サービスがダウンした
{: #ts-aiospayloadapidown}

### 概説
{: #ts-pladov}

- 状態: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- お客様への影響: お客様は外部サービス (Azur や Amazon など) からこのサービスにペイロードを書き込めないので、分析用の現行データを取得できません。
- モニタリング・システム:
- 依存項目: IBM Event Stream

### kubectl の構成
{: #ts-pladkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-pladvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ペイロード・ロギング・サービスがダウンした
{: #ts-aiospayloaddown}

### 概説
{: #ts-plsdov}

- 状態: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- お客様への影響: お客様は外部サービス (Azur や Amazon など) からこのサービスにペイロードを書き込めないので、分析用の現行データを取得できません。
- モニタリング・システム:
- 依存項目: IBM Event Stream

### kubectl の構成
{: #ts-plsdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-plsdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running   1          6h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} スケジューリング・サービスがダウンした
{: #ts-aiosscheddown}

### 概説
{: #ts-ssdov}

- 状態: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: N/A

### kubectl の構成
{: #ts-ssdkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}`:8443) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-ssdvr}

1.  以下のコマンドでポッドの状況を確認します。

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} redis サービスがダウンした
{: #ts-aiosredisdown}

### 概説
{: #ts-redov}

- 状態: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: N/A

### kubectl の構成
{: #ts-redkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-redvr}

1.  以下のコマンドでポッドの状況を確認します。

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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。以下の例では、ポッドとして `aios-redis-server-6f4c55fd75-nlrr4` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## etcd サービスがダウンした
{: #ts-etcddown}

### 概説
{: #ts-etcov}

- 状態: etcd_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、要求の分析、ペイロードの保管など)。
- モニタリング・システム:
- 依存項目: なし

### kubectl の構成
{: #ts-etckc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### 確認/リカバリーのステップ
{: #ts-etcvr}

1.  以下のコマンドでポッドの状況を確認します。

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

    3 つの etcd ポッドがあって、それぞれの状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。ポッドが実行中の段階になっていない場合は、エラーも表示されます。ポッドが実行中の段階になっていない場合の状況として考えられるケースを以下にまとめます。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。上記のコマンドを実行して、詳細情報を表示してください。ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。クラスターで CPU やメモリーを使い尽くしたのかもしれません。その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドを要求しても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。この場合も、kubectl describe ... で得られる情報が役立ちます。ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。3 つのことを確認してください。

      - イメージの名前が正しいかどうか。
      - イメージをリポジトリーにプッシュしたかどうか。
      - 手動の `docker pull` によってクラスターにイメージをプルできるかどうか。

    - **ポッドがクラッシュしたか、正常な状態でない**

      まず、現在のコンテナーのログを調べます。
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      以前のコンテナーがクラッシュしていた場合は、以下のコマンドでそのコンテナーのクラッシュ・ログにアクセスできます。
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      たいていは、ポッドが正常に開始していない理由がログに含まれています。ログの情報に基づいて問題を解決してください。どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## イベント・ストリームのダッシュボードの作成
{: #ts-createdashes}

### 概説
{: #ts-dshov}

- この資料では、AI Open Scale サービスをモニターするための新しいダッシュボードの作成方法を説明します。

### kubectl の構成
{: #ts-dshkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  IBM Cloud Private コンソールから kubectl 構成を使用する
    - ICP クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 必要に応じて、名前空間を `aiopenscale` から `es` に変更します。
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### イベント・ストリームの表示
{: #ts-dshve}

イベント・ストリームは幾つかのサービスで構成されています。各サービスの詳細については、サブフォルダーを参照してください。

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

## {{site.data.keyword.aios_short}} モニタリングの使用
{: #ts-aiosusemonitor}

### 概説
{: #ts-omov}

- この資料では、AI Open Scale サービスをモニターするための新しいダッシュボードの作成方法を説明します。

### ダッシュボードのセットアップ
{: #ts-omsd}

- ibm-aiopenscale-x86_64-1.0.0.tar.gz から aios-dashboard.json ファイルを取得します。このファイルは `utils` ディレクトリーにあります。
- ICP クラスター (`https://${ICP Host}:8443`) にログインします
- `「メニュー」` > `「プラットフォーム」` > `「モニタリング」`を選択します
- `「ホーム」`アイコンをクリックします
- `「ダッシュボードのインポート」`メニュー項目をクリックします
- `「.json ファイルのアップロード」`ボタンをクリックして、対象の aios-dashboard.json をポイントします
- prometheus 入力フィールドのために `prometheus` を選択します

### ダッシュボードの表示
{: #ts-omvd}

ダッシュボードには幾つかの行があります。各行の詳細については、下記の情報を参照してください。

- クラスター合計使用量

  この行には、クラスター全体の CPU 使用量、メモリー使用量、ファイル・システム使用量が表示されます。速度計が緑色の場合は、クラスターが正常な状態になっています。そうでない場合は、クラスターにノードを追加するか、他のデプロイメントのために不要なポッドを終了してください。

- 可用性 (サービス別)

  この行には各サービスの可用性が表示されます。左上のパネルで、準備ができているコンテナーの合計数を確認できます。速度計が緑色 100% の場合は、{{site.data.keyword.aios_short}} が健全な状態になっています。そうでない場合は、右側のテーブルを見て、ダウンしているサービスを確認し、そのサービスを稼働状態にするためのアクションを実行してください。ほかにも、コンテナーが正常に開始していない理由を診断するのに役立つ {{site.data.keyword.aios_short}} 運用手順書があります。上部のパネルの下には各サービスのパネルがあります。緑色のラインは、準備ができているコンテナーの数です。赤色のラインは、要求されたコンテナーの数です。

- CPU (サービス別)

  この行には各サービスの CPU 使用量が表示されます。緑色のラインは、各コンテナーが使用している CPU コアの数です。赤色のラインは、各コンテナーが使用できる CPU コアの制限数です。緑色のラインが赤色のラインに近づきすぎている場合は、コンテナーであまりにも多くの CPU リソースが消費されている理由を確認してください。必要に応じて、そのコンテナーの CPU の制限数を増やすこともできます。そのためには、デプロイメントを編集して CPU の制限数を更新します。
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  例:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- メモリー (サービス別)

  この行には各サービスのメモリー使用量が表示されます。緑色のラインは、各コンテナーが使用しているメモリーの量の数です。赤色のラインは、各コンテナーが使用できるメモリーの量です。緑色のラインが赤色のラインに近づきすぎている場合は、コンテナーであまりにも多くのメモリーが消費されている理由を確認してください。必要に応じて、そのコンテナーのメモリー量を増やすこともできます。そのためには、デプロイメントを編集してメモリーの制限値を更新します。
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  例:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- ファイル・システム (サービス別)

  この行には各サービスのファイル・システム使用量が表示されます。緑色のラインがファイル・システムの使用量です。緑色のラインが伸び続けている場合は、コンテナーを調べて、ファイル・システムの使用量が増え続けている理由を確認してください。必要に応じて、上記の Slack チャネルに連絡してサポートを求めることもできます。

- イメージとバージョン

  この行には、AI Open Scale で使用されているすべてのイメージとバージョンが表示されます。
