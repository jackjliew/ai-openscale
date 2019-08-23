---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: release notes, what's new 

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

# 新機能
{: #rn-relnotes}

このドキュメントでは、{{site.data.keyword.aios_full_notm}} の新しい項目について概説します。
{: shortdesc}

## 2019 年 7 月 9 日
{: #rn-9jul2019}

{{site.data.keyword.aios_short}} には、以下の新機能と変更があります。

- __*オンライン・ヘルプの更新と拡張*__: {{site.data.keyword.aios_short}} オンライン・ヘルプが最近再編成され、目次ペインでトピックを見つけやすくなりました。また、多くの新しいトピックが作成され、拡張されました。

   詳しくは、[インサイトの取得](/docs/services/ai-openscale?topic=ai-openscale-io-ov)と[ライト・プランから有料プランへの {{site.data.keyword.aios_short}} のアップグレード](/docs/services/ai-openscale?topic=ai-openscale-cf-upgrade)を参照してください。
   
## 2019 年 7 月 2 日
{: #rn-2jul2019}

{{site.data.keyword.aios_short}} には、以下の新機能と変更があります。

- __*ドリフトの検出*__: ![ベータ・タグ](images/beta.png)

  {{site.data.keyword.aios_short}} はドリフトの検出をサポートするようになりました。

   詳しくは、[ドリフトの検出](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)を参照してください。

- __*Microsoft Azure ML Service のサポート*__: {{site.data.keyword.aios_short}} は Microsoft Azure ML Service をサポートするようになりました。これにより、Azure ML サービスの AI モデルを {{site.data.keyword.aios_short}} の公平性、正確性、および説明性に統合できるようになりました。

   詳しくは、[Microsoft Azure ML Service のフレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)を参照してください。

- __*改善されたワークフロー*__: {{site.data.keyword.aios_short}} は、クリック数の低減と説明性の向上により効率的に作業できるようにワークフローを改善することに注力してきました。 ナビゲーション・パネルで現在いる場所を確認できるので、簡単に構成タスク間を行き来できるようになりました。

   詳しくは、[デプロイメントでのモニタリングのための準備](/docs/services/ai-openscale?topic=ai-openscale-mo-config)を参照してください。

- __*複数の機械学習プロバイダー*__: 機械学習プロバイダーまたはエンジンを 1 つだけに制限すべき理由はありません。 最新バージョンの {{site.data.keyword.aios_short}} では、複数のプロバイダーを追加できるので、各プロバイダーの独自の機能を利用したり既存のアプリの利用を継続したりできます。

   詳しくは、[複数の機械学習エンジンのサポート](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)を参照してください。

- __*すぐに使用可能な指標の追加*__: このバージョンの {{site.data.keyword.aios_short}} では、公平性、モデル性能、動作、パフォーマンス、および分析に関する多くの新しい指標が追加されました。 これまでより多くの指標がすぐに使用可能となっています。

   詳しくは、[モデル性能の指標の概要](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)を参照してから、[公正性](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)、[パフォーマンス](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)、[分析](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)、および[動作](/docs/services/ai-openscale?topic=ai-openscale-behavior-ovr)をクリックして参照してください。

- __*バイアスに関する作業の効率化*__: バイアス構成として公平性属性が推奨され、値が自動設定されるので、デプロイされたモデル内で、{{site.data.keyword.aios_short}} が公平性のしきい値違反の可能性を検出する場所が簡単にわかります。 推奨された特徴量を受け入れてモニターすることも、値を変更することもできます。

   詳しくは、[公平性指標の概要](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)を参照してください。

## 2019 年 6 月 11 日
{: #rn-11June2019}

本サービスに対する以下の新しい項目と変更点があります。

- __*更新されたダッシュボード機能*__: {{site.data.keyword.aios_short}} ダッシュボードで、いくつかの改訂が行われました。 この新しいバージョンには以下の改良が組み込まれています。

    - 新しいヘルプ・パネルを使用して、StackOverflow や IBM Support などのリソースを容易に検出可能 
    - ダッシュボードでのグローバリゼーションの有効化
    - ユーザビリティーの拡張

## 2019 年 6 月 7 日
{: #rn-7June2019}

本サービスに対する以下の新しい項目と変更点があります。

- __*拡張されたコマンド・ライン・インターフェース*__: コマンド・ライン・インターフェース ibm-ai-openscale-cli が更新され、バージョン 0.2.148 がリリースされました。 この新しいバージョンには以下の改良が組み込まれています。

    - 品質指標の履歴の更新による、OpenScale でサポートされる新しい品質指標の全範囲の組み込み
    - IBM Db2 の使用時に SSL 証明書を直接指定するためのサポート
    - 新しい ibm-ai-openscale 2.1.8 Python SDK のサポート
    - その他のバグ修正および安定度の改善

   `pip install -U ibm-ai-openscale-cli` コマンドを実行して PyPI からインストールし、`ibm-ai-openscale-cli --help` コマンドを実行して使用法のヘルプを取得します。 詳しくは、[PyPI プロジェクト・ページ](https://pypi.org/project/ibm-ai-openscale-cli)を参照してください。

## 2019 年 5 月 29 日
{: #rn-29May2019}

本サービスに対する以下の新しい項目と変更点があります。

- __*バイアスの視覚化の機能拡張*__: ![ベータ・タグ](images/beta.png) バイアスの視覚化には以下のビューが含まれます。 

    - ペイロードと摂動済み: 選択した時間に関して受信した評価要求が含まれます。評価に必要な最小数のレコードがなかった場合には、それに加えてそれより前の時間のレコードも含まれます。 モニター対象の特徴量の値に変更があると、追加の摂動/合成されたレコードも含まれます。このレコードはモデルの応答のテストに使用されます。
    - ペイロード: 選択した時間に関してモデルが受信した実際の評価要求。
    - 訓練: モデルを訓練するための訓練データ・レコード。
    - バイアス緩和済み: ランタイムと摂動済みのデータを処理した後のバイアス緩和アルゴリズムの出力。

   詳しくは、[バイアスの視覚化](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz)を参照してください。

- __*バイアス緩和された出力の正解率の計算*__: 正解率の計算には、バイアス緩和された出力が含まれます。 バイアス緩和されたモデルの正解率と実動モデルの正解率を比較することができます。

   詳しくは、[正解率](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view)を参照してください。

- __*複数の機械学習エンジンのサポート*__: {{site.data.keyword.aios_short}} では、[Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) によってプロビジョニングを実行する場合に、単一インスタンス内で複数の機械学習エンジンを使用できます。

   詳しくは、[複数の機械学習エンジンのサポート](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)を参照してください。

- __*国際化対応*__: {{site.data.keyword.aios_short}} は、ローカライズ・バージョンをサポートし、サポートされている言語の処理データを含んでいます。 {{site.data.keyword.aios_short}} のユーザー・インターフェース、ドキュメンテーション、およびエラー・メッセージは、現時点では次の言語に翻訳されています。 
    - ドイツ語
    - フランス語
    - イタリア語
    - スペイン語
    - ブラジル・ポルトガル語
    - 日本語
    - 中国語 (簡体字)
    - 中国語 (繁体字)
    - 韓国語

   制限事項を含む詳細については 、[{{site.data.keyword.aios_short}} でサポートされる言語](/docs/services/ai-openscale?topic=ai-openscale-sl-langs)を参照してください。

- __*{{site.data.keyword.pm_full}} フレームワークの機能拡張*__: {{site.data.keyword.aios_short}} は、{{site.data.keyword.pm_full}} エンジンの scikit-learn と XGBoost のフレームワークをサポートするようになりました。

   詳しくは、[{{site.data.keyword.pm_full}} フレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml)を参照してください。

## 2019 年 4 月 25 日
{: #rn-25April2019}

本サービスに対する以下の新しい項目と変更点があります。

使いやすさが改善され、セキュリティーが更新されたことに加えて、新しい項目の開発も目まぐるしく進められています。 ここ数週間に追加または拡張された {{site.data.keyword.aios_short}} の項目には、以下のものがあります。

- __*自動セットアップ・ツアー*__: {{site.data.keyword.aios_short}} 環境をセットアップする新しいツアー形式の方法。 [自動セットアップ](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)を使用して、サービスをプロビジョンし、モデルをダウンロードして構成することができます。 このオプションは、{{site.data.keyword.aios_short}} の新しいインスタンスを作成すると表示されます。
- __*ベータ版への切り替え*__: ![ベータ・タグ](images/beta.png) **「ベータ版を試す」**という新しいトグルを使用すると、ベータ版の環境で作業することができます。この環境で、最新の項目や新しい機能をすべて確認できます。 内容が気に入らない場合は、 **「元のバージョンに戻る」**をクリックするだけで、元の環境に切り替えることができます。 構成やモニターは影響を受けません。 以下の機能は、現行のベータ・プログラムの一部です。
    - __*混同行列*__: [混同行列で表示される](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx)のは、誤検出と検出漏れです。 セルをクリックして、フィードバック・レコードのサブセットを表示します。

## 2019 年 4 月 10 日
{: #rn-10April2019}

- __*Express Path ツールでの顧客モデルのサポート*__: {{site.data.keyword.aios_short}} へのオンボーディング・プロセスを自動化します。

   詳しくは、[ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/) を参照してください。


## 2019 年 3 月 5 日
{: #rn-5March2019}

本サービスに対する以下の新しい項目と変更点があります。

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*新しい信用リスク・モデル*__: 新しい信用リスク・モデルの例/チュートリアルは、すべての予測エンジンに対応しています。 詳しくは、[入門](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted)および[追加リソース](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov)・トピックを参照してください。

- __*バイアス緩和の計算*__: {{site.data.keyword.aios_short}} で作成されたバイアスが緩和されたモデルと実動モデルの間で切り替えることができます。 詳しくは、[実動モデルとバイアスが緩和されたモデル](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb)および[バイアス緩和の処理の流れについて](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)を参照してください。

## 2019 年 2 月 22 日
{: #rn-22February2019}

本サービスに対する以下の新しい項目と変更点があります。

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*UI の更新*__: JSON ファイルをインポートして、サブスクリプションの作成時にすべてのモニターと特徴量をプログラムで構成できます。 構成ファイルをエクスポートすることもできます。 詳しくは、[JSON ファイルを使用したデプロイメント・サブスクリプションの構成](/docs/services/ai-openscale?topic=ai-openscale-cf-ov)トピックを参照してください。

## 2019 年 2 月 7 日
{: #rn-7February2019}

本サービスに対する以下の新しい項目と変更点があります。

直前のリリース以降に追加または拡張された {{site.data.keyword.aios_short}} の項目には以下のものがあります。

- __*UI の更新*__: {{site.data.keyword.aios_short}} ユーザー・インターフェースでいくつかの機能が改善されています。これには、[オンデマンドで公平性と正解率を確認する](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)方法や、[公平性を示す詳細なグラフ](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)からトランザクション・リストを表示できる機能などがあります。

- __*説明性の機能強化*__: 関連する肯定的 (PP) 値および関連する否定的 (PN) 値ですべての数値の適合率/位取りが同一になりました。

- __*Db2 SSL サポート*__: {{site.data.keyword.aios_short}} で DB2 資格情報を使って自己署名証明書 (Base-64 エンコード) を受け渡す機能がサポートされました。

- __*{{site.data.keyword.Bluemix}} Database のサポート*__: {{site.data.keyword.aios_short}} で Compose for PostgreSQL と Db2 の他に、Databases for PostgreSQL がサポートされるようになりました。

## 2018 年 12 月 14 日
{: #rn-14December2018}

本サービスに対する以下の新しい項目、変更点、既知の問題があります。

ベータ版以降に追加または拡張された {{site.data.keyword.aios_short}} の特徴量には以下のものがあります。

- __*一般出荷版*__: {{site.data.keyword.aios_full_notm}} の一般出荷版 (GA) リリースは {{site.data.keyword.Bluemix}} Standard (有料) のプランです。

- __*{{site.data.keyword.icp4dfull_notm}} V1.2*__: {{site.data.keyword.wos4d_full}} V1.2 を使用している場合は、[インストール・チェックリスト](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#install)の文書 (インストール手順を含む) を参照してください。

- __*モデル・タイプのサポート*__: {{site.data.keyword.aios_short}} では、{{site.data.keyword.pm_full}} の AI モデル・デプロイメントに加えて、Microsoft Azure、Amazon SageMaker、カスタム環境のモデル・デプロイメントもサポートしています。 詳しくは、[サポートされるモデル・タイプ](/docs/services/ai-openscale?topic=ai-openscale-in-ov)を参照してください。

- __*無料の「lite」データベース*__: 無料の「lite」管理対象データベースには、{{site.data.keyword.aios_short}} を使い始めるために必要なすべてのものが用意されています。 詳しくは、[{{site.data.keyword.aios_short}} の価格設定プラン](https://{DomainName}/catalog/services/watson-openscale){: external}を参照してください。

- __*バイアス・モニタリング*__: タイプ `float` または `double` の保護属性と、線形回帰モデルでのバイアス検出がサポートされています。 また、{{site.data.keyword.aios_short}} では自動的に AI モデルのバイアスを排除できます。 詳しくは、[公平性について](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。

- __*説明性*__: 回帰モデル、Python 関数、および補足的な対比的説明をサポートしています。 詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

- __*データ・ストア*__: {{site.data.keyword.pm_full}} に依存せずにモデル性能モニタリングを利用できます。また、自分が所有するデータベース (Db2、Postgres、Db2 on Cloud など) を使用できます。

- __*UI の拡張*__: {{site.data.keyword.aios_short}} UI の機能が向上し、実行時ヒストグラム分布が表示されるようになりました。そこには、モデル ID とバージョン管理を切り替える訓練データ用のトグルと、ヒストグラムに基づくトランザクション ID テーブルがあります。 詳しくは、[特定の時間のデータの視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)を参照してください。

- __*代替チュートリアル・セットアップ・オプション*__: 必要な {{site.data.keyword.Bluemix}} サービスのプロビジョニングと構成を自動化し、IBM {{site.data.keyword.aios_full}} アプリケーション (サンプル・データを含む) を表示するために、Python モジュールをインストールして実行できます。 [{{site.data.keyword.aios_short}} をセットアップするための Python モジュールのインストール](/docs/services/ai-openscale?topic=ai-openscale-as-module)を参照してください

## 2018 年 9 月 17 日
{: #rn-17September2018}

- **ベータ・プレビュー・リリース** - {{site.data.keyword.aios_full_notm}} ベータ・プレビュー・リリースが公開されました。

<p>&nbsp;</p>

## 次のステップ
{: #relnotes-in-next}

まだご不明な点がありますか?

- [制限](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [既知の問題](/docs/services/ai-openscale?topic=ai-openscale-rn-12ki#cloud-limitations)
