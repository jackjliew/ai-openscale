---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

このドキュメントでは、{{site.data.keyword.aios_full_notm}} の新しい項目について概説します。
{: shortdesc}

## 2019 年 5 月 29 日
{: #rn-29May2019}

本サービスに対する以下の新しい項目と変更点があります。

- __*バイアスの視覚化の機能拡張*__: ![ベータ・タグ](images/beta.png) バイアスの視覚化には以下のビューが含まれます。 

    - ペイロードと摂動済み: 選択した時間に関して受信した評価要求が含まれます。評価に必要な最小数のレコードがなかった場合には、それに加えてそれより前の時間のレコードも含まれます。モニター対象の特徴量の値に変更があると、追加の摂動/合成されたレコードも含まれます。このレコードはモデルの応答のテストに使用されます。
    - ペイロード: 選択した時間に関してモデルが受信した実際の評価要求。
    - 訓練: モデルを訓練するための訓練データ・レコード。
    - バイアス緩和済み: ランタイムと摂動済みのデータを処理した後のバイアス緩和アルゴリズムの出力。

   詳しくは、[バイアスの視覚化](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz)を参照してください。

- __*バイアス緩和された出力の正解率の計算*__: 正解率の計算には、バイアス緩和された出力が含まれます。バイアス緩和されたモデルの正解率と実動モデルの正解率を比較することができます。

   詳しくは、[正解率](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view)を参照してください。

- __*複数の機械学習エンジンのサポート*__: {{site.data.keyword.aios_short}} では、プロビジョニングがコマンド・ライン・インターフェース (CLI) を使用して実行される場合は、単一のインスタンス内で複数の機械学習エンジンがサポートされます。

   詳しくは、[ModelOps CLI ツール](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mop)を参照してください。

- __*国際化対応*__: {{site.data.keyword.aios_short}} は、ローカライズ・バージョンをサポートし、サポートされている言語の処理データを含んでいます。{{site.data.keyword.aios_short}} のユーザー・インターフェース、ドキュメンテーション、およびエラー・メッセージは、現時点では次の言語に翻訳されています。 
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

   詳しくは、[WML フレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml)を参照してください。

## 2019 年 4 月 25 日
{: #rn-25April2019}

本サービスに対する以下の新しい項目と変更点があります。

使いやすさが改善され、セキュリティーが更新されたことに加えて、新しい項目の開発も目まぐるしく進められています。 ここ数週間に追加または拡張された {{site.data.keyword.aios_short}} の項目には、以下のものがあります。

- __*自動セットアップ・ツアー*__: {{site.data.keyword.aios_short}} 環境をセットアップする新しいツアー形式の方法。 [自動セットアップ](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)を使用して、サービスをプロビジョンし、モデルをダウンロードして構成することができます。 このオプションは、{{site.data.keyword.aios_short}} の新しいインスタンスを作成すると表示されます。
- __*ベータ版への切り替え*__: ![ベータ・タグ](images/beta.png) **「ベータ版を試す」**という新しいトグルを使用すると、ベータ版の環境で作業することができます。この環境で、最新の項目や新しい機能をすべて確認できます。 内容が気に入らない場合は、 **「元のバージョンに戻る」**をクリックするだけで、元の環境に切り替えることができます。 構成やモニターは影響を受けません。 以下の機能は、現行のベータ・プログラムの一部です。
    - __*混同行列*__: [混同行列で表示される](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx#it-conf-mtx)のは、誤検出と検出漏れです。 セルをクリックして、フィードバック・レコードのサブセットを表示します。

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

- __*IBM Cloud Database のサポート*__: {{site.data.keyword.aios_short}} で Compose for PostgreSQL と Db2 の他に、Databases for PostgreSQL がサポートされるようになりました

## 2018 年 12 月 14 日
{: #rn-14December2018}

本サービスに対する以下の新しい項目、変更点、既知の問題があります。

ベータ版以降に追加または拡張された {{site.data.keyword.aios_short}} の特徴量には以下のものがあります。

- __*一般出荷版*__: {{site.data.keyword.aios_full_notm}} の一般出荷版 (GA) は IBM Cloud Standard (有料) のプランです。

- __*IBM Cloud Private for Data V1.2*__: IBM Cloud Private for Data V1.2 で {{site.data.keyword.aios_short}} を使用している場合は、[インストール・チェックリスト](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)の文書 (インストール手順を含む) を参照してください

- __*モデル・タイプのサポート*__: {{site.data.keyword.aios_short}} では、Watson Machine Learning の AI モデル・デプロイメントに加えて、Microsoft Azure、Amazon SageMaker、カスタム環境のモデル・デプロイメントもサポートしています。 詳しくは、[サポートされるモデル・タイプ](/docs/services/ai-openscale?topic=ai-openscale-in-ov)を参照してください。

- __*無料の「lite」データベース*__: 無料の「lite」管理対象データベースには、{{site.data.keyword.aios_short}} を使い始めるために必要なすべてのものが用意されています。 詳しくは、[{{site.data.keyword.aios_short}} の価格プラン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/watson-openscale){: new_window} を参照してください。

- __*バイアス・モニタリング*__: タイプ `float` または `double` の保護属性と、線形回帰モデルでのバイアス検出がサポートされています。 また、{{site.data.keyword.aios_short}} では自動的に AI モデルのバイアスを排除できます。 詳しくは、[公平性について](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。

- __*説明性*__: 回帰モデル、Python 関数、および補足的な対比的説明をサポートしています。 詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

- __*データ・ストア*__: Watson Machine Learning に依存しない品質モニタリングを利用できます。また、自分が所有するデータベース (Db2、Postgres、Db2 on Cloud など) を使用できます。

- __*UI の拡張*__: {{site.data.keyword.aios_short}} UI の機能が向上し、実行時ヒストグラム分布が表示されるようになりました。そこには、モデル ID とバージョン管理を切り替える訓練データ用のトグルと、ヒストグラムに基づくトランザクション ID テーブルがあります。 詳しくは、[特定の時間のデータの視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)を参照してください。

- __*代替チュートリアル・セットアップ・オプション*__: 必要な IBM Cloud サービスのプロビジョニングと構成を自動化し、IBM {{site.data.keyword.aios_full}} アプリケーション (サンプル・データを含む) を表示するために、Python モジュールをインストールして実行できます。 [{{site.data.keyword.aios_short}} をセットアップするための Python モジュールのインストール](/docs/services/ai-openscale?topic=ai-openscale-as-module)を参照してください

## 2018 年 9 月 17 日
{: #rn-17September2018}

- **ベータ・プレビュー・リリース** - {{site.data.keyword.aios_full_notm}} ベータ・プレビュー・リリースが公開されました。

<p>&nbsp;</p>

## 次のステップ
{: #relnotes-in-next}

まだご不明な点がありますか?

- [制限](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [既知の問題](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
