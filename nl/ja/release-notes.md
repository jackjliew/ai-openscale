---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: release notes, what's new 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 新機能
{: #rn-relnotes}

このドキュメントでは、{{site.data.keyword.aios_full_notm}} の新しい項目と既知の問題について概説します。
{: shortdesc}

## 2019 年 3 月 5 日
{: #rn-5March2019}

本サービスに対する以下の新しい項目と変更点があります。

### 新しい項目と変更点
{: #rn-5March2019nf}

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*新しい信用リスク・モデル*__: 新しい信用リスク・モデルの例/チュートリアルは、すべての評価エンジンに対応しています。詳しくは、[入門](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted)および[追加リソース](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov)・トピックを参照してください。

- __*バイアス緩和の計算*__: {{site.data.keyword.aios_short}} で作成されたバイアスが排除されたモデルと実動モデルの間で切り替えることができます。詳しくは、[実動モデルとバイアスが排除されたモデル](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb)および[バイアス緩和の処理の流れについて](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)を参照してください。

## 2019 年 2 月 22 日
{: #rn-22February2019}

本サービスに対する以下の新しい項目と変更点があります。

### 新しい項目と変更点
{: #rn-22February2019nf}

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*UI の更新*__: JSON ファイルをインポートして、サブスクリプションの作成時にすべてのモニターと項目をプログラムで構成できます。構成ファイルをエクスポートすることもできます。詳しくは、[JSON ファイルを使用したデプロイメント・サブスクリプションの構成](/docs/services/ai-openscale?topic=ai-openscale-cf-ov)トピックを参照してください。

## 2019 年 2 月 7 日
{: #rn-7February2019}

本サービスに対する以下の新しい項目と変更点があります。

### 新しい項目と変更点
{: #rn-7February2019nf}

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*UI の更新*__: {{site.data.keyword.aios_short}} ユーザー・インターフェースでいくつかの機能が改善されています。これには、[オンデマンドで公平性と正解率を確認する](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)方法や、[公平性を示す詳細なグラフ](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)からトランザクション・リストを表示できる機能などがあります。

- __*説明性の機能強化*__: 関連する肯定的 (PP) 値および関連する否定的 (PN) 値ですべての数値の適合率/位取りが同一になりました。

- __*Db2 SSL サポート*__: {{site.data.keyword.aios_short}} で DB2 資格情報を使って自己署名証明書 (Base-64 エンコード) を受け渡す機能がサポートされました。

- __*IBM Cloud Database のサポート*__: {{site.data.keyword.aios_short}} で Compose for PostgreSQL と Db2 の他に、Databases for PostgreSQL がサポートされるようになりました

### 既知の問題
{: #rn-7February2019ki}

- **カスタム ML サービス・インスタンス**

    - 現行の [Python モジュール](/docs/services/ai-openscale?topic=ai-openscale-as-module)では、カスタム・サービス・インスタンスに対して説明性が機能しません。これは、カスタム・サービス・インスタンスでは応答データに数値による予測が必要ですが、このモジュール・スクリプトにはそれが含まれていないためです。

## 2018 年 12 月 14 日
{: #rn-14December2018}

本サービスに対する以下の新しい項目、変更点、既知の問題があります。

### 新しい項目と変更点
{: #rn-12nf}

ベータ版以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*一般出荷版*__: {{site.data.keyword.aios_full_notm}} の一般出荷版 (GA) は IBM Cloud Standard (有料) のプランです。

- __*IBM Cloud Private for Data V1.2*__: IBM Cloud Private for Data V1.2 で {{site.data.keyword.aios_short}} を使用している場合は、[インストール・チェックリスト](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)の文書 (インストール手順を含む) を参照してください

- __*モデル・タイプのサポート*__: {{site.data.keyword.aios_short}} では、Watson Machine Learning の AI モデル・デプロイメントに加えて、Microsoft Azure、Amazon SageMaker、カスタム環境のモデル・デプロイメントもサポートしています。詳しくは、[サポートされるモデル・タイプ](/docs/services/ai-openscale?topic=ai-openscale-in-ov)を参照してください。

- __*無料の「lite」データベース*__: 無料の「lite」管理対象データベースには、{{site.data.keyword.aios_short}} を使い始めるために必要なすべてのものが用意されています。詳しくは、[{{site.data.keyword.aios_short}} の価格プラン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/watson-openscale){: new_window} を参照してください。

- __*バイアス・モニタリング*__: タイプ `float` または `double` の保護属性と、線形回帰モデルでのバイアス検出がサポートされています。また、{{site.data.keyword.aios_short}} では自動的に AI モデルのバイアスを排除できます。詳しくは、[公平性について](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。

- __*説明性*__: 回帰モデル、Python 関数、および補足的な対比的説明をサポートしています。詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

- __*データ・ストア*__: Watson Machine Learning に依存しない品質モニタリングを利用できます。また、自分が所有するデータベース (Db2、Postgres、Db2 on Cloud など) を使用できます。

- __*NeuNetS (ベータ版)*__: IBM Neural Network Synthesizer (NeuNetS) がベータ版として利用できるようになりました (パブリック・クラウドのみ)。詳しくは、[NeuNetS の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window} を参照してください。

- __*UI の拡張*__: {{site.data.keyword.aios_short}} UI の機能が向上し、実行時ヒストグラム分布が表示されるようになりました。そこには、モデル ID とバージョン管理を切り替えるトレーニング・データ用のトグルと、ヒストグラムに基づくトランザクション ID テーブルがあります。詳しくは、[特定の時間のデータの視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)を参照してください。

- __*代替チュートリアル・セットアップ・オプション*__: 必要な IBM Cloud サービスのプロビジョニングと構成を自動化し、IBM {{site.data.keyword.aios_full}} アプリケーション (サンプル・データを含む) を表示するために、Python モジュールをインストールして実行できます。[{{site.data.keyword.aios_short}} をセットアップするための Python モジュールのインストール](/docs/services/ai-openscale?topic=ai-openscale-as-module)を参照してください

### 既知の問題
{: #rn-12ki}

- **Microsoft Azure**

    - 2 種類の Azure Machine Learning Web サービスのうち、{{site.data.keyword.aios_short}} では `New` タイプのみがサポートされています。`Classic` タイプはサポートされていません。

    - __*デフォルトの入力名を使用する必要があります*__: Azure Web サービスではデフォルトの入力名は `input1` です。現時点ではこのフィールドは {{site.data.keyword.aios_short}} で必須であり、欠落している場合は {{site.data.keyword.aios_short}} が機能しません。

      Azure Web サービスでデフォルト名を使用していない場合は、入力フィールド名を`「input1」`に変更してください。これでコードが機能するようになります。

- **AWS SageMaker**

    - __*BlazingText アルゴリズムはサポートされていません*__: AWS SageMaker BlazingText アルゴリズム入力ペイロード・フォーマットは、{{site.data.keyword.aios_short}} の現行リリースではサポートされていません。

## 2018 年 9 月 17 日
{: #rn-17September2018}

### 新しい項目と変更点
{: #rn-17nf}

- **ベータ・プレビュー・リリース** - {{site.data.keyword.aios_full_notm}} ベータ・プレビュー・リリースが公開されました。
