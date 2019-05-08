---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-15"

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
{:download: .download}

# インストールのチェックリスト
{: #inst-install-icp}

{{site.data.keyword.aios_short}} ツールを {{site.data.keyword.icpfull}} for Data にインストールする方法について説明します。
{: shortdesc}

{{site.data.keyword.icpfull_notm}} 環境は Kubernetes ベースのコンテナー・プラットフォームであり、アプリケーションとサービスに関連付けられたワークロードを素早く近代化し、自動化するのに役立ちます。独自のインフラストラクチャーとデータ・センターにおいて開発、デプロイすることができ、リスクの軽減と脆弱性の最小化に役立ちます。

## ハードウェア要件
{: #inst-hw}

[System requirements for {{site.data.keyword.icpfull_notm}} for Data ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.1.0/com.ibm.icpdata.doc/zen/install/reqs-ent.html){: new_window} で、必ず最新の要件を確認してください。

### オペレーティング・システムの要件
{: #inst-hwo}

| オペレーティング・システム | 最小レベル | ハードウェア | ビット・レベル
|:---|:---:|:---:|:---:
|Red Hat Enterprise Linux (RHEL) Server 7 | 7.5 | x86-64 | 64-Exploit ||

### 3 ノード構成のハードウェア要件とソフトウェア要件
{: #inst-hwt}

この構成では、少なくとも 4 つのサーバー (物理マシンまたは仮想マシンのいずれか) が必要です。この場合、3 つがマスター・ノードとワーカー・ノードとして動作 (例えば、`node1` が `master1` と `worker1` の両方として動作) し、1 つがロード・バランサーとして動作します。

| ノード・タイプ | サーバーの数 (BM/VM) | CPU | RAM | ディスク・パーティション
|:---|:---:|:---:|:---:|:---
| マスター/ワーカー | 3 | 32 個のコア | 128 GB | /[root] ファイル・システム用に 100 GB |
| | | | | インストール・パス用に、少なくとも 400 GB がマウントされた XFS ファイル・システム。このパスは、各ノード上のインストーラー・データ・ストレージ用です。SSD などのハイパフォーマンス・ディスク・ドライブでなければなりません。 |
| | | | | データ・パス用に、少なくとも 400 GB がマウントされた XFS ファイル・システム。このデータ・パスは、ユーザー・データ・ストレージ用です。この量を提供すると、400 GB の使用可能なスペースを持つユーザー・データのレプリケーションが 3 つできます。ユーザーのワークロードに応じて、追加のディスク・スペースが必要な場合があります。 |
| | | | | オプション: Docker デバイス・マッパー用の 200 GB のロウ・ディスク。このロウ・ディスクを提供しない場合は、インストール・パス用に少なくとも 600 GB が必要です。 |
| ロード・バランサー | 1 | 少なくとも 4 個のコア | 8GB | 少なくとも 100GB。1 つのロード・バランサーに対するこの最小要件は、{{site.data.keyword.pm_full}} を使用するクライアントの場合です。これは、Google または AWS がホストするサービスなど、ロード・バランシングが他のプロバイダーによって処理される構成の場合は必要ありません。 |

### 6 ノード構成のハードウェア要件とソフトウェア要件
{: #inst-hws}

この構成では、少なくとも 7 つのサーバー (物理マシンまたは仮想マシンのいずれか) が必要です。この場合、3 つが`マスター`・ノード、3 つが`ワーカー`・ノードとしてそれぞれ動作し、1 つがロード・バランサーとして動作します。

| ノード・タイプ | サーバーの数 (BM/VM) | CPU | RAM | ディスク・パーティション
|:---|:---:|:---:|:---:|:---
| マスター | 3 | 16 個のコア | 32 GB | /[root] ファイル・システム用に 100 GB |
| | | | | インストール・パス用に、400 GB がマウントされた XFS ファイル・システム。このパスは、各ノード上のインストーラー・データ・ストレージ用です。SSD などのハイパフォーマンス・ディスク・ドライブでなければなりません。 |
| | | | | データ・パス用に、400 GB がマウントされた XFS ファイル・システム。このデータ・パスは、ユーザー・データ・ストレージ用です。この量を提供すると、500 GB の使用可能なスペースを持つユーザー・データのレプリケーションが 3 つできます。ユーザーのワークロードに応じて、追加のディスク・スペースが必要な場合があります。 |
| | | | | オプション: Docker デバイス・マッパー用の 200 GB のロウ・ディスク。このロウ・ディスクを提供しない場合は、インストール・パス用に少なくとも 600 GB が必要です。 |
| ワーカー | 3 | 16 個のコア | 128 GB | /[root] ファイル・システム用に 100 GB |
| | | | | インストール・パス用に、400 GB がマウントされた XFS ファイル・システム。このパスは、各ノード上のインストーラー・データ・ストレージ用です。|
| | | | | データ・パス用に、400 GB がマウントされた XFS ファイル・システム。このデータ・パスは、クラスター内の 3 つの各ワーカー・ノード上のユーザー・データ・ストレージ用です。この量を提供すると、400 GB の使用可能なスペースを持つユーザー・データのレプリケーションが 3 つできます。ユーザーのワークロードに応じて、追加のディスク・スペースが必要な場合があります。 |
| | | | | オプション: Docker デバイス・マッパー用の 200 GB のロウ・ディスク。このロウ・ディスクを提供しない場合は、インストール・パス用に少なくとも 600 GB が必要です。 |

### (オプション) Db2 Warehouse の要件
{: #inst-hwd}

Db2 Warehouse データベースを {{site.data.keyword.icpfull_notm}} for Data クラスターにデプロイする予定の場合は、以下のような仕様で専用のワーカー・ノードを作成する必要があります。

| ノード・タイプ | サーバーの数 (BM/VM) | CPU | RAM | ディスク・パーティション
|:---|:---:|:---:|:---|:---
| ワーカー | 1 | 8 個のコア | 64 GB | 最低限の構成が記述された 1 つのデータベース用に TB のストレージが適切です。 |
| | | | コア対メモリーの最小比率: 1:8 | 複数の Db2 Warehouse ポッド・デプロイメント、または同じストレージ・オブジェクト・クラスを使用するその他のワークロードでは、追加のストレージ・スペースが必要です。 |
| | | | パフォーマンス向上のためのコア対メモリーの推奨比率: 1:16 | 実行するスコアリングの量によりますが、スターターとして 5 TB を強くお勧めします。 |

## ソフトウェア要件
{: #inst-sw}

[IBM パスポート・アドバンテージ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/passportadvantage/pao_customer.html){: new_window} から、パーツ・ナンバー別に、該当するパッケージをダウンロードします。

下記のパーツ・ナンバーは、{{site.data.keyword.icpfull_notm}} for Data 用の {{site.data.keyword.aios_full_notm}} をダウンロードしたのが 2019 年 4 月 16 日より前であるか、その日以降であるかによって異なります。必ず正しいパーツ・ナンバーを選択してください。
{: important}

1.  {{site.data.keyword.icpfull_notm}} for Data ({{site.data.keyword.icpfull_notm}} で稼働)。

    - **2019 年 4 月 16 日_より前_**: スタンドアロンの {{site.data.keyword.icpfull_notm}} for Data パッケージをダウンロードします (パーツ・ナンバー *CNY56EN*)。これは `.bin` ファイルで、{{site.data.keyword.icpfull_notm}} 3.1.2 プラットフォームと {{site.data.keyword.icpfull_notm}} for Data 1.2 Enterprise Edition の両方が含まれています。パーツ・ナンバーは、{{site.data.keyword.icpfull_notm}} for Data Enterprise Edition パッケージのものです。

    - **2019 年 4 月 16 日_より後_**: {{site.data.keyword.icpfull_notm}} for Data バージョン 1.2.1.1 をダウンロードします。これは、{{site.data.keyword.icpfull_notm}} プラットフォームにバンドルされなくなりました (パーツ・ナンバー *CC11KML*)。

1.  {{site.data.keyword.icpfull_notm}} for Data Watson Machine Learning Extension パッケージ

    - **2019 年 4 月 16 日_より前_** - バージョン 1.2.0.1 に関連したファイルをダウンロードします (パーツ・ナンバー *CC092EN*)。

    - **2019 年 4 月 16 日_より後_** - バージョン 1.2.1 に関連したファイルをダウンロードします (パーツ・ナンバー *CC0ENEN*)。

1.  IBM Event Streams V2018.3.1 for Linux on x86 64-bit Multilingual

    - パーツ・ナンバー *CNXJ8ML* をダウンロードします。

1.  IBM Db2 Warehouse ({{site.data.keyword.icpfull_notm}} for Data 1.2.1 用) (オプション)

    - バージョン 3.3.0 に関連したファイルをダウンロードします (パーツ・ナンバー *CC0EMEN*)。

1.  {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} for Data (Linux 64 ビット・システム)

    - バージョン 1.0.2 に関連したファイルをダウンロードします (パーツ・ナンバー *CC16SEN*)。


## 構成の要件
{: #inst-conf}

{{site.data.keyword.icpfull_notm}} for Data をインストールする際は、以下の構成に関する項目に注意する必要があります。

- すべてのクラスター・ノードのパブリック IP アドレスが静的でなければなりません。
- すべてのクラスター・ノードのプライベート IP アドレスが静的でなければなりません。あるマシンのリブートから別のものに IP アドレスが変更されている場合、そのシステムを使用することはできません。
- すべてのクラスター・ノードで、root ログインが可能でなければなりません。
- インストール時には、すべてのクラスター・ノードで、root パスワードが同じでなければなりません。
- ロード・バランサー・ノードで、以下のポートが開かれている必要があります。

|ポート |  |  |  |  |
|:---:|:---:|:---:|:---:|:---:
| 8001 | 8443 | 9443 | 8500 | 8600 |
| 80 | 443 | 31843 | 32448 | 31962 |
| 31030 | 31031 | 30836 | 31002 | 32006 |

- DB2 Warehouse を使用する場合は、ロード・バランサー上で DB2 ノードも開かれている必要があります。

## {{site.data.keyword.icpfull_notm}} for Data が**_既にインストールされている_** 場合
{: #inst-exist}

{{site.data.keyword.icpfull_notm}} for Data クラスターが既にインストールされている場合は、[Upgrading IBM Cloud Private for Data](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.1/com.ibm.icpdata.doc/zen/install/upgrade-overview.html) の説明に従って、組み込みの {{site.data.keyword.icpfull_notm}} および {{site.data.keyword.icpfull_notm}} for Data コンポーネントをアップグレードします。以下のことを確認してください。

- {{site.data.keyword.icpfull_notm}} をバージョン 3.1.0 から 3.1.2 にアップグレードする
- {{site.data.keyword.icpfull_notm}} for Data をバージョン 1.2.0 から 1.2.1 にアップグレードする

ノードがプロビジョンされたら、下記の [Watson Machine Learning パッケージのインストール](#inst-wml)を続行します。

## {{site.data.keyword.icpfull_notm}} for Data が**_まだインストールされていない_** 場合
{: #inst-icp4d}

IBM Knowledge Center の [Overview of IBM Cloud Private for Data ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.1/com.ibm.icpdata.doc/zen/overview/overview.html) のトピックを確認します。

次に、自動化スクリプトを使用して、{{site.data.keyword.aios_short}} を初めから作成してインストールします。[ハードウェア要件](#inst-hw)を満たすマシンのセットがあることを前提としています。

スクリプトは、IBM SoftLayer 内の仮想プライベート・クラウド用に最適化されています。
{: note}

- {{site.data.keyword.aios_short}} tarball をダウンロードして、`master1` ノードとして使用するマシン (例えば `/openscale`) に保存します。

- 以下のコマンドを実行して、自動化スクリプトを抽出します。

  ```bash
  tar -xzf <OpenScale.tar.gz file> utils/prepCluster.zip
  cd utils
  unzip prepCluster.zip
  cd install
  ```

- インストール・ディレクトリーの `README.md` の説明に従って、{{site.data.keyword.icpfull_notm}} for Data、Watson Machine Learning、Event Streams、および {{site.data.keyword.aios_short}} を作成、検証、およびインストールします。オプションで、[Db2 Warehouse インストール・ガイド](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_1.2.0/com.ibm.icpdata.doc/zen/admin/download-db-pkg.html)を参照して、Db2 をインストールします。


## Watson Machine Learning パッケージのインストール
{: #inst-wml}

IBM Knowledge Center の説明に従って、[Watson Machine Learning アドオン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/extend-ai-analytics.html#extend-ai-analytics__wml) をインストールします。

ICP4D への Watson Machine Learning モジュールのインストールの終了時に、ロード・バランサー・システム上の `/etc/haproxy/haproxy.cfg` に、以下の行を追加します。

  ```bash
  frontend wml
      bind *:31002
      mode tcp
      option tcplog
      use_backend wml

  backend wml
      mode tcp
      balance roundrobin
      server server1 <master01-IP>:31002
      server server2 <master02-IP>:31002
      server server3 <master03-IP>:31002

  frontend wml-envoy
      bind *:32006
      mode tcp
      option tcplog
      use_backend wml-envoy

  backend wml-envoy
      mode tcp
      balance roundrobin
      server server1 <master01-IP>:32006
      server server2 <master02-IP>:32006
      server server3 <master03-IP>:32006
  ```

  この IP アドレスを、すべてのクラスター・マスター・ノードの IP アドレスに変更します。
  {: note}

  この構成ファイル内のサーバー名は、常に `server1`、`server2`、`server3`、といった順序で始まります。
  {: note}

上記の変更を保存した後で、次のコマンドを実行して、変更を有効にします。

  ```bash
  systemctl restart haproxy
  systemctl status -l haproxy
  ```

次に、コマンド出力にエラーがないことを確認します。以下に、参照出力の例を示します。

  ```bash
  haproxy.service - HAProxy Load Balancer
   Loaded: loaded (/usr/lib/systemd/system/haproxy.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2018-12-10 09:48:06 CST; 6ms ago
 Main PID: 73659 (haproxy-systemd)
   CGroup: /system.slice/haproxy.service
           ├─73659 /usr/sbin/haproxy-systemd-wrapper -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid
           └─73661 /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds

  Dec 10 09:48:06 yssd.yong.cloud systemd[1]: Started HAProxy Load Balancer.
  Dec 10 09:48:06 yssd.yong.cloud systemd[1]: Starting HAProxy Load Balancer...
  Dec 10 09:48:06 yssd.yong.cloud haproxy-systemd-wrapper[73659]: haproxy-systemd-wrapper: executing /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -p /run/haproxy.pid -Ds
  ```


## (オプション) IBM Db2 Warehouse パッケージのインストール
{: #inst-db2}

IBM Knowledge Center の [Downloading the database installation package ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/download-db-pkg.html#download-db2-warehouse-pkg) の説明に従います。

## {{site.data.keyword.icpfull_notm}} for Data クラスターへのログイン
{: #log-cluster}

次のコマンドを入力します。

`cloudctl login`

プロンプトが出されたら、ICP 管理者のユーザー名とパスワードを入力します。

## IBM Event Streams V2018.3.1 for Linux および {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} のインストール
{: #inst-es-aios}

### Event Streams のインストール
{: #inst-es}

1.  IBM Event Streams V2018.3.1 for Linux on x86 64-bit Multilingual tarball を {{site.data.keyword.icpfull_notm}} for Data クラスター `master-1 node` 上のディレクトリー (例えば `/ibm/ES`) にコピーします。

1.  {{site.data.keyword.aios_full_notm}} for {{site.data.keyword.icpfull_notm}} 1.0.2 tarball を{{site.data.keyword.icpfull_notm}} for Data クラスター `master-1 node` 上のディレクトリー (例えば `/ibm/AIOS`) に untar します。

1.  コマンド・ライン・ウィンドウから、Docker レジストリーと {{site.data.keyword.aios_full_notm}} クラスターにログインします。

1.  {{site.data.keyword.icpfull_notm}} for Data クラスター `master-1 node` から、{{site.data.keyword.aios_short}} tarball 内の `install_es.sh` パッケージを使用して Event Streams をインストールします。以下に例を示します。

    ```bash
    cd /ibm/AIOS
    ./install_es.sh -f /ibm/ES/[<Event_Streams_tarball_file_name>]
    ```

1.  `install_es.sh` の実行が完了すると、次のメッセージが表示されます。以下のように、メッセージで概説されているステップを実行してから、次のステップに進みます。

    ```bash
    以下のステップに従って、HAProxy ロード・バランサーを介して Event Stream のポートを公開します。

    1. `${HAPROXY_OUTPUT}` の内容を `${LOAD_BALANCER_IP}` 上の `/etc/haproxy/haproxy.cfg` に追加します。

    2. `${LOAD_BALANCER_IP}` 上で `systemctl restart haproxy` を実行して、HAProxy ロード・バランサーを再始動します。

    別のロード・バランサーを使用する場合は、Event Stream のポート 31703、31105、31094、32180、および 32036 をマスター・ノードに公開するように、そのロード・バランサーを構成します。
    ```

### {{site.data.keyword.aios_full_notm}} のインストール
{: #inst-aios}

1.  {{site.data.keyword.aios_short}} をインストールします。

    組み込みの {{site.data.keyword.icpfull_notm}} for Data インストールを使用してクラスターがインストールされていない場合は、以下のステップを実行する必要があります。
    {: important}

    - {{site.data.keyword.aios_short}} tarball に含まれている `common.sh` ファイル内の環境変数設定を更新します。

    - 手動によるストレージのプロビジョニングを使用している場合は、{{site.data.keyword.aios_short}} コンポーネントに必要な永続ボリュームを手動で作成する必要があります。

        - ご使用の環境の {{site.data.keyword.aios_short}} tarball に含まれている `utils/etcd-pvc-template.yaml` ファイルをカスタマイズします。別のストレージ・タイプを使用している場合は、テンプレート内の `nfs` セクションを置き換えます。

          - NFS ボリュームを使用するには、以下のようにします。

            - `NFS_SERVER_IP` をご使用の NFS ホストの IP アドレスに置き換えます。

            - NFS マウント・ポイントが異なる場合は、`/data/aios-etcd-0`、`/data/aios-etcd-1`、および `/data/aios-etcd-2` を置き換えます。

            - `kubectl create namespace aiopenscale` を実行します。

            - `kubectl -n aiopenscale create -f etcd-pvc-template.yaml` を実行して、`PersistentVolume` と `PersistentVolumeClaim` を作成します。

    - `StorageClass` で `DynamicProvisioning` を使用している場合は、`oketi-gluster` を `common.sh` ファイル内の `StorageClass` 名に置き換えます。

    以下のように、インストールを実行します。

    ```bash
    ./install_aios.sh
    ```

  インストールの際に、ご使用条件を読み、そのご使用条件、{{site.data.keyword.icpfull_notm}} for Data 管理者の `username` と `password`、{{site.data.keyword.icpfull_notm}} 管理者の `username` と `password`、Event Streams のリリース名、および Event Streams の名前空間を受け入れるよう、プロンプトが出されます。

  可能な限り、デフォルト値が提供されます。本書で定義されているように、{{site.data.keyword.icpfull_notm}} for Data、Watson Machine Learning、および Event Streams のインストール・ステップに従う場合は、デフォルト値を使用してください。

## インストールの確認
{: #inst-po}

- {{site.data.keyword.icpfull_notm}} for Data [Management Console ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_2.1.0.3/manage_cluster/cfc_gui.html) にログインし、画面の右上にあるアイコンをクリックして、*「アドオン (Add-ons)」*ページに移動します。

  または

- `https://[Load Balancer IP]:31843/zen/#/addons` と入力して、{{site.data.keyword.aios_short}} アドオンをクリックし、{{site.data.keyword.aios_short}} UI を開きます。

  {{site.data.keyword.aios_short}} UI は、{{site.data.keyword.icpfull_notm}} UI の {{site.data.keyword.aios_full_notm}} にログインした後で、`https://[Load Balancer IP]:31843/aiopenscale` を使用して起動することもできます。

## アンインストール・ステップ
{: #inst-un}

1.  {{site.data.keyword.aios_short}} のインストール元となった、{{site.data.keyword.icpfull_notm}} for Data クラスター `master-1 node` ホスト上のディレクトリー (例えば `ibm/aios`) に移動します。

1.  `./uninstall_aios.sh` を実行します。

アンインストールの際に、{{site.data.keyword.icpfull_notm}} 管理者の `username` と `password` を入力するよう、プロンプトが出されます。

## 次のステップ
{: #inst-next}

{{site.data.keyword.aios_short}} ツールを使用して、AI モデルのバイアスと正確度をモニターします。

- {{site.data.keyword.aios_short}} サービスについて詳しくは、[概要](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-abt-about)を参照してください。
- 動作を自分で確認するには、[入門](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started)チュートリアルのステップに従ってください。
