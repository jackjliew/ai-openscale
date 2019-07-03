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

# トラブルシューティング
{: #ts-trouble}

## {{site.data.keyword.aios_full}} のよくある問題
{: #ts-trouble-common}

{{site.data.keyword.aios_full}} on Cloud と {{site.data.keyword.wos4d_full}} の両方でよく見られる問題を以下に示します。

### ペイロード分析が正しく表示されない
{: #ts-trouble-common-payloadfileformat}

- 状態: 以下のエラー・メッセージが表示されます。
  - エラー・コード: AIQDT0044E
  - エラー・テキスト: 使用禁止文字 `"` が列名 `<column name>` に含まれている (Forbidden character `"` in column name `<column name>`)

- 状態: ペイロード分析の正常な処理のために、{{site.data.keyword.aios_short}} は、二重引用符 (") を含む列名のペイロードをサポートしていません。これは、CSV 形式および JSON 形式の評価ペイロードとフィードバック・データにも該当します。
- 解決方法: ペイロード・ファイルの列名から二重引用符 (") を削除してください。

## {{site.data.keyword.wos4d_full}} に固有の問題
{: #ts-trouble-icp}

以下の問題は、{{site.data.keyword.wos4d_full}} に固有のものです。

## バイアス/公平性サービスがダウンした
{: #ts-bfdown}

### 概要
{: #ts-bfdov}

- 状態: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

    たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## {{site.data.keyword.aios_short}} サービスがダウンした
{: #ts-aiosdown}

### 概要
{: #ts-odov}

- 状態: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する

    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

        ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

        - クラスターにさらにノードを追加します。

        - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
        ```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

    たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## {{site.data.keyword.aios_short}} 構成サービスがダウンした
{: #ts-aiosconfigdown}

### 概要
{: #ts-ocdov}

- 状態: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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

  `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-configuration-554f548667-7l782` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ダッシュボード・サービスがダウンした
{: #ts-aiosdashdown}

### 概要
{: #ts-oddov}

- 状態: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---
## データマート・サービスがダウンした
{: #ts-datamartdown}

### 概要
{: #ts-dmdov}

- 状態: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## 説明性サービスがダウンした
{: #ts-expdown}

### 概要
{: #ts-esdov}

- 状態: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} フィードバック・サービスがダウンした
{: #ts-aiosfeedbackdown}

### 概要
{: #ts-fsdov}

- 状態: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**2/2**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ディスカバリー・サービスがダウンした
{: #ts-aiosdiscdown}

### 概要
{: #ts-dsdov}

- 状態: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  オプション 2: {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} nginx サービスがダウンした
{: #ts-aiosnginxdown}

### 概要
{: #ts-nsdov}

- 状態: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ペイロード・ロギング API サービスがダウンした
{: #ts-aiospayloadapidown}

### 概要
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} ペイロード・ロギング・サービスがダウンした
{: #ts-aiospayloaddown}

### 概要
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} スケジューリング・サービスがダウンした
{: #ts-aiosscheddown}

### 概要
{: #ts-ssdov}

- 状態: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}`:8443) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## {{site.data.keyword.aios_short}} redis サービスがダウンした
{: #ts-aiosredisdown}

### 概要
{: #ts-redov}

- 状態: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    状況が **running** で、完全に準備ができた状態 (**1/1**) になっていることを確認します。  以下の例では、ポッドとして `aios-redis-server-6f4c55fd75-nlrr4` を使用します。

1.  ポッドが実行中の段階になっていない場合は、ポッドの詳細情報を表示します。

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o <format> コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## etcd サービスがダウンした
{: #ts-etcddown}

### 概要
{: #ts-etcov}

- 状態: etcd_micro_service_is_down:
- お客様への影響: お客様はどの機能も使用できなくなります (新しいインスタンスの構成、リクエストの分析、ペイロードの保管など)。
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
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
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

    このコマンドを実行すると、ポッドの詳細情報が表示されます。  ポッドが実行中の段階になっていない場合は、エラーも表示されます。  ポッドが実行中の段階になっていない場合は、ポッドで以下の状況が発生している可能性があります。

    - **ポッドが処理待ちになっている**

      ポッドが **Pending** になっていると、ノードでのスケジューリングができません。  たいていは、スケジューリングに必要ないずれかのタイプのリソースが不足していることが原因です。  上記のコマンドを実行して詳細情報を取得してください。 ポッドのスケジューリングができない理由についてのメッセージがスケジューラーから生成されているはずです。 クラスターで CPU やメモリーを使い尽くしたのかもしれません。 その場合は、以下のことを試してみてください。

      - クラスターにさらにノードを追加します。

      - 処理待ちのポッドの処理を可能にするために不要なポッドを終了します。
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - ポッドの容量がノードの容量を超えていないことを確認します。 例えば、全ノードの容量が cpu:1 なのに、cpu:1.1 のポッドをリクエストしても、スケジューリングはできません。

      ノードの容量は、kubectl get nodes -o `<format>` コマンドで確認できます。 必要な情報を抽出するためのコマンド・ラインの例を以下に示します。
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **ポッドが待ち状態になっている**

      ポッドが **Waiting** の状態で止まっている場合は、ワーカー・ノードでのスケジューリングは済んでいますが、そのマシンでまだ実行できない状況です。 この場合も、kubectl describe ... で得られる情報が役立ちます。 ポッドが **Waiting** になる最も一般的な原因は、イメージをプルできないということです。 3 つのことを確認してください。

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

      たいていは、ポッドが正常に開始していない理由がログに含まれています。  ログの情報に基づいて問題を解決してください。  どの方法でもうまくいかない場合は、エスカレーション・ステップに進んでください。

---

## イベント・ストリームのダッシュボードの作成
{: #ts-createdashes}

### 概要
{: #ts-dshov}

- この資料では、{{site.data.keyword.aios_full}} サービスをモニターするための新しいダッシュボードの作成方法を説明します。

### kubectl の構成
{: #ts-dshkc}

kubectl クライアントを構成するには、2 つの方法があります。

1.  cloudctl ツールを使用する

    cloudctl がラップトップにある場合は、以下のコマンドを実行して kubectl を構成します。
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    `${username}`、`${password}`、`${ICP Host}` は、実際の値に置き換えてください。  例えば、以下のようにします。
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  {{site.data.keyword.icpfull}} コンソールから kubectl 構成を使用する
    - {{site.data.keyword.icpfull}} クラスター (`https://${ICP Host}:8443`) にログインします
    - **丸い人**のアイコン > **「クライアントの構成」**を選択します
    - **「クリップボードにコピー」**アイコンをクリックして、構成情報をクリップボードにコピーします
    - 必要に応じて、名前空間を `aiopenscale` から `es` に変更します。
    - 構成情報をコマンド・ラインに貼り付けて、**Enter** を押します。

### イベント・ストリームの表示
{: #ts-dshve}

イベント・ストリームは幾つかのサービスで構成されています。  各サービスの詳細については、サブフォルダーを参照してください。

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

### 概要
{: #ts-omov}

- この資料では、{{site.data.keyword.aios_full}} サービスをモニターするための新しいダッシュボードの作成方法を説明します。

### ダッシュボードのセットアップ
{: #ts-omsd}

- ibm-aiopenscale-x86_64-1.0.0.tar.gz から aios-dashboard.json ファイルを取得します。  このファイルは `utils` ディレクトリーにあります。
- ICP クラスター (`https://${ICP Host}:8443`) にログインします
- `「メニュー」` > `「プラットフォーム」` > `「モニタリング」`を選択します
- `「ホーム」`アイコンをクリックします
- `「ダッシュボードのインポート」`メニュー項目をクリックします
- `「.json ファイルのアップロード」`ボタンをクリックして、対象の aios-dashboard.json をポイントします
- prometheus 入力フィールドのために `prometheus` を選択します

### ダッシュボードの表示
{: #ts-omvd}

このダッシュボードは、以下の行で構成されています。

- クラスター合計使用量

  この行には、クラスター全体の CPU 使用量、メモリー使用量、ファイル・システム使用量が表示されます。 速度計は、クラスターが正常な状態であるかどうかを示しています。 正常な状態でないことを示している場合は、クラスターにさらにノードを追加するか不要なポッドを終了して、他のデプロイメントのための余地を作ってください。

- 可用性 (サービス別)

  この行には各サービスの可用性が表示されます。  初期パネルで、準備ができているコンテナーの合計数を確認できます。  速度計が 100% を示している場合、{{site.data.keyword.aios_short}} は正常な状態です。  そうでない場合は、テーブルを見て、ダウンしているサービスを確認し、そのサービスを稼働状態にするためのアクションを実行してください。  ほかにも、コンテナーが正常に開始していない理由を診断するのに役立つ {{site.data.keyword.aios_short}} 運用手順書があります。  初期パネルの後に個々のサービスのパネルが続きます。 異なる行に作業可能なコンテナーの数と要求されたコンテナーの数が表示されます。

- CPU (サービス別)

  この行には各サービスの CPU 使用量が示され、各コンテナーが使用している CPU コアの数と各コンテナーが使用できる CPU コアの制限数が含まれています。  これらの値が近すぎる場合は、そのコンテナーが CPU リソースを大量に消費している理由を調べてください。  必要に応じて、そのコンテナーの CPU の制限数を増やすこともできます。そのためには、デプロイメントを編集して CPU の制限数を更新します。
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  例:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- メモリー (サービス別)

  この行には、各サービスのメモリー使用量が示され、各コンテナーが使用しているメモリーと各コンテナーが使用できるメモリーが含まれています。  これらの値が近すぎる場合は、そのコンテナーがメモリーを大量に消費している理由を調べてください。  必要に応じて、そのコンテナーのメモリー量を増やすこともできます。そのためには、デプロイメントを編集してメモリーの制限値を更新します。
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  例:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- ファイル・システム (サービス別)

  この行には各サービスのファイル・システム使用量が表示されます。  モニターでファイル・システム使用量が絶えず増加していることが示されている場合は、ファイル・システム使用量が増え続けている理由をコンテナーで調べてください。  必要に応じて、前述の Slack チャネルに連絡して、さらに支援を受けることもできます。

- イメージとバージョン

  この行には、{{site.data.keyword.aios_full}} で使用されているすべてのイメージとバージョンがリスト表示されます。
