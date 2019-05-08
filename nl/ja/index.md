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

# 概要
{: #abt-about}

{{site.data.keyword.aios_full}} は、AI 活用アプリケーションのためのエンタープライズ規模の環境です。企業のビジネスの規模に応じて、AI がどのように構築、活用されているかを可視化し、投資収益率 (ROI) の向上を実現します。
{: shortdesc}

## 実装
{: #abt-implement}

{{site.data.keyword.aios_short}} は、以下のように実装します。

- **{{site.data.keyword.aios_short}} の構成**: 使いやすいグラフィカル環境を使用して、[ペイロード・ロギング・データベースをセットアップ](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)し、AI モデルとデプロイメントが保管される [Watson Machine Learning インスタンス](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cwml-wml)をセットアップします。

- **モニターの操作**: デプロイメントごとに、{{site.data.keyword.aios_short}} でそのデプロイメントをモニターする方法を構成します。以下をモニターできます。

    - [公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)
    - [正確度](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)

- **モニター対象データの表示と編集**: {{site.data.keyword.aios_short}} [ダッシュボード](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-iov-insights)を使用すると、重要な洞察の表示や、デプロイメントの問題の特定が容易になります。各モニター対象フィーチャーの個々のデータ・ポイントを可視化することによって、さらに詳細が明らかになります。

## 制限
{: #abt-limits}

- 現行リリースでサポートされるのは、1 つのデータベース、1 つの Watson Machine Learning インスタンス、および 1 つの {{site.data.keyword.aios_short}} のインスタンスのみです。

- データベースと Watson Machine Learning インスタンスは、同じ {{site.data.keyword.cloud_notm}} アカウントにデプロイする必要があります。

- {{site.data.keyword.aios_short}} では、PostgreSQL または Db2 データベースを使用して、モデル・デプロイメントの出力とリトレーニング・データを保管します。Db2 のライト・プランは現在サポートされていません。
    

- {{site.data.keyword.aios_short}} のインスタンス当たりにデプロイされるモデルが 20 個というライセンス制限があります。

- 現在、サイズが 1 MB より大きいイメージの説明は生成できません。

## サポートされるモデル・タイプ
{: #abt-models}

表 1. モデルのサポートの詳細

| アルゴリズム | **公平性** | **自動バイアス除去** | **説明** | **正確度** |
|:---|:---:|:---:|:---:|:---:|
| **構造化分類** | あり | あり<sup>1</sup> | あり<sup>1</sup> | あり |
| **構造化回帰**     | あり | 近日公開 | あり | あり |
| **テキストの分類**       | なし - アクティブな調査トピック | なし - アクティブな調査トピック | あり<sup>1</sup> | なし |
| **イメージの分類**      | なし - アクティブな調査トピック | なし - アクティブな調査トピック | あり<sup>1</sup> | なし ||
{: caption="モデルのサポートの詳細" caption-side="top"}

<sup>1</sup> モデル / フレームワークで予測の確率が出力された場合

## サポートされるフレームワーク
{: #abt-frame}

表 1. フレームワークのサポートの詳細

| アルゴリズム | **すぐに使用可能なサポート** | **[カスタム環境](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ccust-custom)または Python 機能のサポート** |
|:---|:---:|:---:|
| **構造化分類** | Spark mllib on WML、AWS Sagemaker Native<sup>1</sup>、Azure ML Studio Native | Scikit-Learn、XGboost、SPSS, Keras、Tensorflow、Pytorch、Caffe、またはその他の選択したフレームワーク |
| **構造化回帰**     | Spark mllib on WML、AWS Sagemaker Native<sup>1</sup>、Azure ML Studio Native | Scikit-Learn、XGboost、SPSS, Keras、Tensorflow、Pytorch、Caffe、またはその他の選択したフレームワーク |
| **テキストの分類**       | Spark mllib on WML | 近日公開: Keras、Tensorflow、Pytorch、Caffe、およびその他多数 |
| **イメージの分類**      | Keras on WML | 近日公開: Keras、Tensorflow、Pytorch、Caffe、およびその他多数 ||
{: caption="フレームワークのサポートの詳細" caption-side="top"}

<sup>1</sup> AWS 組み込みアルゴリズム

## ブラウザー・サポート
{: #abt-browser}

{{site.data.keyword.aios_short}} サービス・ツールには、{{site.data.keyword.cloud_notm}} で必要なものと同じレベルのブラウザー・ソフトウェアが必要です。詳しくは、{{site.data.keyword.cloud_notm}} の[前提条件](/docs/overview?topic=overview-prereqs-platform#browsers)のトピックを参照してください。

## ModelOps CLI ツール
{: #abt-mopscli}

[{{site.data.keyword.aios_short}} CLI モデル操作ツール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} を使用すると、機械学習モデルのライフサイクル管理に関連したタスクを実行できます。このツールは、{{site.data.keyword.cloud_notm}} CLI ツールを補完するもので、[機械学習プラグイン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window} によって拡張されています。

## Python クライアント
{: #abt-python}

[{{site.data.keyword.aios_short}} Python クライアント![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/){: new_window} は、{{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.aios_short}} サービスで直接処理できる Python ライブラリーです。{{site.data.keyword.aios_short}} クライアント UI の代わりに Python クライアントを使用すると、ロギング・データベースの直接的な構成、機械学習エンジンのバインド、デプロイメントの選択とモニターが可能になります。このような方法での Python クライアントの使用例については、[{{site.data.keyword.aios_short}} サンプル・ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks) を参照してください。

## 次のステップ
{: #abt-next}

- サービスを[開始](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started)します。
- [API 参照資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/ai-openscale){: new_window} を表示します。

他に不明な点がありますか? [IBM ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window} にお問い合わせください。
