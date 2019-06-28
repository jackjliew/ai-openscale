---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# 製品情報
{: #in-ov}

{{site.data.keyword.aios_full}} は、AI 活用アプリケーションに対応したエンタープライズ・グレードの環境です。企業のビジネスの規模に応じて、AI の構築方法と利用方法、さらに、AI が投資収益率の向上に貢献する方法を可視化します。
{: shortdesc}

<p>&nbsp;</p>

## 実装
{: #in-imp}

ここでは {{site.data.keyword.aios_short}} を実装する方法について説明します。

- **{{site.data.keyword.aios_short}}** の構成: 使いやすいグラフィカル環境を利用して、[ペイロード・ロギング・データベース](/docs/services/ai-openscale?topic=ai-openscale-connect-db)と、AI モデルとデプロイメントが格納される [Watson Machine Learning インスタンス](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)をセットアップします。

- **モニターの使用**: 各デプロイメントで、{{site.data.keyword.aios_short}} が対象デプロイメントをモニターする方法を構成します。 以下についてモニターできます。

    - [公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [正解率](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - [パフォーマンス](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **モニター対象データの表示と編集**: {{site.data.keyword.aios_short}}[ダッシュボード](/docs/services/ai-openscale?topic=ai-openscale-io-ov)を利用すると、主要なインサイトを簡単に確認し、デプロイメントの問題を特定できます。 各モニター対象の特徴量のそれぞれのデータ・ポイントを可視化することによって、詳細を確認できます。

<p>&nbsp;</p>

## 制限
{: #in-lim}

- 現行リリースでサポートされているのは、1 つのデータベース、1 つの {{site.data.keyword.pm_full}} インスタンス、1 つの {{site.data.keyword.aios_short}} インスタンスのみです

- データベースと {{site.data.keyword.pm_full}} インスタンスは、同じ {{site.data.keyword.cloud_notm}} アカウントにデプロイする必要があります。

- Lite (無料) プランには、以下の月次制限があります。

    - モニター対象は 2 つのデプロイ済みモデル
    - 説明対象は 20 個のトランザクション
    - 50,000 件のペイロード・レコード (累積)
    - 50,000 件のフィードバック・レコード (累積)

- {{site.data.keyword.aios_short}} は PostgreSQL データベースまたは Db2 データベースを使用して、モデル関連データ (フィードバック・データ、評価ペイロード) や計算された指標を保管します。 Db2 の Lite プランは現在サポートされていません。

- {{site.data.keyword.aios_short}} のインスタンスあたり、デプロイ済みモデルは 1 ライセンスについて 20 個に制限されています。

- {{site.data.keyword.pm_full}} の場合、機械学習ゲートウェイ経由で送信される摂動済みのイメージのペイロードは、1 MB を超えることはできません。 タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。


<p>&nbsp;</p>

## 既知の問題
{: #rn-12ki}

- **Microsoft Azure**

    - 2 種類の Azure Machine Learning Web サービスのうち、{{site.data.keyword.aios_short}} では `New` タイプのみがサポートされています。 `Classic` タイプはサポートされていません。

    - __*デフォルトの入力名を使用する必要があります*__: Azure Web サービスではデフォルトの入力名は `input1` です。 現時点ではこのフィールドは {{site.data.keyword.aios_short}} で必須であり、欠落している場合は {{site.data.keyword.aios_short}} が機能しません。

      Azure Web サービスでデフォルト名を使用していない場合は、入力フィールド名を`「input1」`に変更してください。これでコードが機能するようになります。

- **AWS SageMaker**

    - __*BlazingText アルゴリズムはサポートされていません*__: AWS SageMaker BlazingText アルゴリズム入力ペイロード・フォーマットは、{{site.data.keyword.aios_short}} の現行リリースではサポートされていません。

- **カスタム ML サービス・インスタンス**

    - 現行の [Python モジュール](/docs/services/ai-openscale?topic=ai-openscale-as-module)では、カスタム・サービス・インスタンスに対して説明性が機能しません。 これは、カスタム・サービス・インスタンスでは応答データに数値による予測が必要ですが、このモジュール・スクリプトにはそれが含まれていないためです。

<p>&nbsp;</p>

## サポートされる機械学習エンジンとフレームワーク
{: #in-fram}

{{site.data.keyword.aios_short}} サービスは、以下の機械学習エンジンをサポートしています。 各ランタイムは、以下のフレームワークで作成されたモデルをサポートします。

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [カスタム](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (ICP のみ)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

完全なサポートには、特定のフレームワーク、問題、データ・タイプ用の以下の項目も含まれます。

- ペイロード・ロギング	
- フィードバック・ロギング	
- パフォーマンスの正解率	
- 実行時のバイアス検出	
- 説明性	
- 自動バイアス緩和

<p>&nbsp;</p>

## ブラウザーのサポート
{: #in-brw}

{{site.data.keyword.aios_short}} サービス・ツールでは、{{site.data.keyword.cloud_notm}} で必要とされるレベルと同じレベルのブラウザー・ソフトウェアが必要です。 詳しくは、{{site.data.keyword.cloud_notm}} の[前提条件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)トピックを参照してください。

<p>&nbsp;</p>

## ModelOps CLI ツール
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI モデル操作ツール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} を使用すると、機械学習モデルのライフサイクル管理に関連するタスクを実行できます。 このツールは {{site.data.keyword.cloud_notm}} CLI ツールを補完するもので、[機械学習プラグイン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window} によって機能強化されます。

<p>&nbsp;</p>

## Python クライアント
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python クライアント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/){: new_window} は、{{site.data.keyword.cloud_notm}} 上で {{site.data.keyword.aios_short}} サービスを直接扱うことができる Python ライブラリーです。 {{site.data.keyword.aios_short}} クライアント UI ではなく Python クライアントを使用すると、ロギング・データベースの構成、機械学習エンジンのバインド、デプロイメントの選択とモニターを直接行うことができます。 例えば、このように Python クライアントを使用する場合には、[{{site.data.keyword.aios_short}} サンプル・ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks) を参照してください。

<p>&nbsp;</p>

## 次のステップ
{: #in-next}

- サービスを[開始](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)します。
- [API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale){: new_window} を参照します。

まだご不明な点がありますか? 

- [新機能](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM にお問い合わせください ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}。
