---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# サポートのためのログ・ファイルの取得
{: #log-files}

{{site.data.keyword.icpfull}} のログ・ファイルを取得し、IBM サポートにそれらのファイルを送信する方法について説明します。
{: shortdesc}

重要な手順は以下のとおりです。

- ICP クラスターにログインします。

    - コマンド・ライン・ツール `cloudctl` をダウンロードし、インストールしたことを確認します。

    - 例えば、以下のようにして、ICP クラスターにログインします。

      ```curl
      cloudctl login -c id-mycluster-account -u <AdminUserName> -p <AdminPassword> -a https://169.60.000.000:1234 --skip-ssl-validation -n aiopenscale
      ```

- ログ・ファイルを取得します。

    - どんなポッドが使用可能かを確認します。

      ```bash
      kubectl get pods --namespace aiopenscale
      ```

以下に、出力例を示します。

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-bias-744df9d95d-slhnp | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-common-api-577b75c445-p9ftk | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-configuration-86b87746f8-nvt5t | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-dashboard-55444db6b6-vfxsz | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-datamart-55fc74474d-9hjw4 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-feedback-59f7c558bd-xgd56 | 2/2 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-ml-gateway-discovery-88c87d548-52ldh | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-nginx-7d7695c447-cm2j6 | 1/1 | Running | 0 | 5d |
| ai-open-scale-ibm-aios-payload-logging-84c794df8-dwsv9 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-payload-logging-api-896674959-hzbq8 | 1/1 | Running | 0 | 1h |
| ai-open-scale-ibm-aios-scheduling-7d6d96545c-2v8s8 | 1/1 | Running | 0 | 1h |
| aios-redis-sentinel-6d5bffbcd8-dnssh | 1/1 | Running | 0 | 5d |
| aios-redis-sentinel-6d5bffbcd8-nss89 | 1/1 | Running | 0 | 5d |
| aios-redis-sentinel-6d5bffbcd8-wg992 | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-24nqn | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-5ntxb | 1/1 | Running | 0 | 5d |
| aios-redis-server-6f4c55fd75-kdqn5 | 1/1 | Running | 0 | 5d |
| etcd-0 | 1/1 | Running | 1 | 5d |
| etcd-1 | 1/1 | Running | 0 | 5d |
| etcd-2 | 1/1 | Running | 0 | 5d ||

- 以下のポッドの場合を示します。

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-common-api-577b75c445-p9ftk           | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-configuration-86b87746f8-nvt5t        | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-dashboard-55444db6b6-vfxsz            | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-datamart-55fc74474d-9hjw4             | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-ml-gateway-discovery-88c87d548-52ldh  | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-nginx-7d7695c447-cm2j6                | 1/1 |      Running |  0  |        5d |
| ai-open-scale-ibm-aios-payload-logging-84c794df8-dwsv9       | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-payload-logging-api-896674959-hzbq8   | 1/1 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-scheduling-7d6d96545c-2v8s8           | 1/1 |      Running |  0  |        1h |
| aios-redis-sentinel-6d5bffbcd8-dnssh                         | 1/1 |      Running |  0  |        5d |
| aios-redis-sentinel-6d5bffbcd8-nss89                         | 1/1 |      Running |  0  |        5d |
| aios-redis-sentinel-6d5bffbcd8-wg992                         | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-24nqn                           | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-5ntxb                           | 1/1 |      Running |  0  |        5d |
| aios-redis-server-6f4c55fd75-kdqn5                           | 1/1 |      Running |  0  |        5d |
| etcd-0                                                       | 1/1 |      Running |  1  |        5d |
| etcd-1                                                       | 1/1 |      Running |  0  |        5d |
| etcd-2                                                       | 1/1 |      Running |  0  |        5d ||

  次のコマンドを実行します。

  ```bash
  kubectl logs <podName> --namespace aiopenscale > pod.log
  ```

- 残りのポッドの場合を示します。

| NAME | READY | STATUS | RESTARTS | AGE
|:---|:---:|:---:|:---:|:---|
| ai-open-scale-ibm-aios-bias-744df9d95d-slhnp                 | 2/2 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h       | 2/2 |      Running |  0  |        1h |
| ai-open-scale-ibm-aios-feedback-59f7c558bd-xgd56             | 2/2 |      Running |  0  |        1h ||

  ```bash
  kubectl logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-hln7h  --container aios-bias --namespace aiopenscale
  ```

  コンテナー名は、前述のコマンドを使用したときに表示されます。

  ```bash
  kubectl logs <podName> --namespace aiopenscale > pod.log
  ```

- ログ・ファイルをパックして、IBM サポートに送信します。

    - ログを zip し、圧縮ファイルを [IBM サポート ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/home/) に送信します。
