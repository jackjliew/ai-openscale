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

# デプロイメントのモニターの準備
{: #mo-config}

{{site.data.keyword.aios_short}} を使用して、追跡しようとしているデプロイメントごとにモニターをセットアップして有効にします。
{: shortdesc}

## デプロイメントの選択
{: #mo-deploy}

1.  最初に、デプロイメントを選択しなければなりません。

    特定のモデルのデプロイメントが複数ある場合、1 つのデプロイメントを構成すると、同じモデルのその他のデプロイメントもすべて構成されます。
    {: note}

    ![デプロイメント選択ページ](images/config-select-deploy.png)

1.  *「モニターの準備 (Prepare for monitoring)」*タイルを選択し、**「開始 (Begin)」**をクリックします。

    ![モニターの準備](images/config-prep-monitor.png)

## データの処理
{: #mo-data}

1.  続いて、モデルとトレーニング・データに関する情報を提供します。**「次へ」**をクリックします。

    ![説明の準備](images/config-what-monitor.png)

1.  ドロップダウン・メニューから、デプロイメントで分析されるデータのタイプを選択し、**「次へ」**をクリックします。

    ![入力タイプの選択](images/config-input-monitor.png)

### 数値/カテゴリー・データ
{: #mo-datan}

数値データかカテゴリー・データの場合、モニターを構成するには、モデルのトレーニング・データに関する情報を提供する必要があります。

  ![構成タイプの選択](images/config-manual-monitor.png)

- **「モニターの手動構成 (Manually configure monitors)」** - トレーニング・データに対する接続情報を提供する必要があります。

    - 以下のように、[アルゴリズムのタイプ](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor#acc-understand)を選択して**「次へ」**をクリックします。

      ![マルチクラス](images/multiclass.png)

      トレーニング・データの形式が、モデルで予期される形式と完全に同じであることを確認してください。例えば、モデルでフィーチャー *Gender* について `M` と `F` が予期されている場合は、トレーニング・データの形式は `Male` と `Female` ではなく `M` と `F` である必要があります。現在 {{site.data.keyword.aios_short}} は Db2 データベースか Cloud Object Storage のロケーションのみサポートしています。
        {: important}

    - ロケーション (`Db2` または `Cloud Object Storage`) を指定してから、以下のようにします。

        - Db2 データベースの場合、以下の情報を入力します。

            - ホスト名または IP アドレス
            - ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

            ![Db2 のトレーニング・データの場所を指定するページ](images/config-train-db2-monitor.png)

        - Cloud Object Storage の場合、以下の情報を入力します。

            - ログイン URL

              ログイン URL は、トレーニング・データがあるバケットの地域設定と一致していなければなりません。次のステップで、トレーニング・データのバケットを指定します。
              {: important}

            - リソース・インスタンス (ID)
            - API 鍵

            ![Cloud Object Storage のトレーニング・データの場所を指定するページ](images/config-train-cos-monitor.png)

    - **「テスト」**ボタンをクリックしてトレーニング・データに接続し、接続が有効であることを確認します。**「次へ」**をクリックします。

    - Db2 データベースまたは Cloud Object Storage 内の、トレーニング・データがある場所を正確に指定します。

        - Db2 データベースの場合、以下のように、モデルで予期される列が含まれるスキーマとトレーニング・テーブルを両方とも選択します。

          ![Db2 のスキーマとトレーニング・テーブルの場所の指定](images/fair-config-table-db2.png)

        - Cloud Object Storage の場合、以下のようにバケットとデータ・セットを選択します。

          ![Cloud Object Storage のデータ・セットの場所の指定](images/fair-config-dset-cos.png)

          **「次へ」**をクリックして、下記のステップ 5 に進みます。

- **「構成ファイルのアップロード (Upload a configuration file)」** - トレーニング・データをプライベートに保とうとしている場合は、このオプションを選択します。カスタム Python ノートブックを使用すると、トレーニング・データ自体へのアクセスを提供せずに、トレーニング・データを分析するための情報を {{site.data.keyword.aios_short}} に提供できます。

  Python ノートブックを実行すると、スキーマ列内の列名だけでなくさまざまな値も収集できます。また、このノートブックを使用して公平性モニターを事前構成できます。

    - [カスタム・ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window} をダウンロードし、その資格情報を独自の資格情報と置き換えます。

    - 該当する個所でご使用のモデルのデータを指定しているか、ノートブックを注意深く検討します。ノートブックを保存します。

    - このノートブックを実行して JSON 形式の構成ファイルを生成します。

    - JSON 構成ファイルをアップロードします。

        ![構成 JSON のアップロード](images/config-json-monitor.png)

    - **「次へ」**をクリックします。

- {{site.data.keyword.aios_short}} は、WML 内のモデルで保管されているメタデータからトレーニング・データを見つけます。このトレーニング・データ内で予測値が含まれているラベル列を選択し、**「次へ」**をクリックします。

  ![列ラベルの選択](images/fair-config-column.png)

- (**SPSS のみ**) 出力データから、確率値のある列を選択します。複数存在する可能性があることに注意してください。**「次へ」**をクリックします。

    ![確率ラベルの選択](images/explain-prob-column.png)

- モデルのトレーニングに使用される列を選択します。この列は、モデル・デプロイメントが要求内で予期するフィーチャーです。**「次へ」**をクリックします。

    ![フィーチャー・ラベルの選択](images/explain-select-column.png)

- 最後に、テキストが含まれていたものの、整数に変換された列を選択します。例えば、元のトレーニング・データの *Gender* に `Male` と `Female` が含まれていたが、現在はそれぞれ `0` と `1` にマップされている場合、トレーニング・データの *Gender* 列には現在 `0` 値と `1` 値が入っています。このような、現在は整数が入っているが、元々はテキスト値が入っていた列を識別します。**「次へ」**をクリックします。

    ![データ・テーブルの選択](images/explain-text-column.png)

### イメージと非構造化テキスト
{: #mo-datai}

- **イメージ**

  入力としてイメージを受け入れるモデルの場合、イメージを (高さ) x (幅) x (チャンネル数) の形式で表す必要があります。ピクセルごとに各ポイントはモノクロームか RGB 値を表します。

- **非構造化テキスト**

   入力としてテキストを受け入れるモデルの場合、そのモデルはテキストのベクトル化された表現ではなくテキスト全体を受け入れると予期されます。

## 構成の検討と保存
{: #mo-save}

選択内容の要約を検討し、**「保存」**をクリックして先に進みます。

SPSS バイナリー・サブスクリプションの場合、**「保存」**のクリック後に別の[ペイロード・ロギング (スコアリング) 要求](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)を行ってからモニターの構成を開始しなければなりません。そうすることにより、[説明可能性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov)の正確さが保証されます。
{: important}

  ![データ・テーブルの選択](images/config-summary-monitor.png)

## 次のステップ
{: #mo-next}

モニターの構成を開始するには、カテゴリーを選択して**「開始 (Begin)」**をクリックします。
