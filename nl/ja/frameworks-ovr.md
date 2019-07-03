---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits

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

# サポートされる機械学習エンジン、フレームワーク、およびモデル
{: #in-fram}

{{site.data.keyword.aios_short}} サービスは、以下の機械学習エンジンをサポートしています。 各ランタイムは、以下のフレームワークで作成されたモデルをサポートします。

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [カスタム](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) ({{site.data.keyword.wos4d_full}}でのみ使用可能)

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

完全なサポートには、特定のフレームワーク、問題、データ・タイプ用の以下の項目も含まれます。

- ペイロード・ロギング	
- フィードバック・ロギング	
- パフォーマンスの正解率	
- 実行時のバイアス検出	
- 説明性	
- 自動バイアス緩和

<p>&nbsp;</p>


## サポートされるモデル・タイプ
{: #abt-models}

表 1. モデルのサポート詳細

| アルゴリズム | **公平性** | **自動バイアス緩和** | **説明** | **正解率** |
|:---|:---:|:---:|:---:|:---:|
| **構造化分類** | はい | はい<sup>1</sup> | はい<sup>1</sup> | はい |
| **構造化回帰**     | はい | 近日公開 | はい | はい |
| **テキスト分類**       | いいえ: アクティブな調査トピック | いいえ: アクティブな調査トピック | はい<sup>1</sup> | いいえ |
| **イメージ分類**      | いいえ: アクティブな調査トピック | いいえ: アクティブな調査トピック | はい<sup>1</sup> | いいえ ||
{: caption="モデルのサポート詳細" caption-side="top"}

<sup>1</sup> モデル/フレームワークが予測確率を出力する場合

<p>&nbsp;</p>

## ブラウザーのサポート
{: #in-brw}

{{site.data.keyword.aios_short}} サービス・ツールでは、{{site.data.keyword.cloud_notm}} で必要とされるレベルと同じレベルのブラウザー・ソフトウェアが必要です。 詳しくは、{{site.data.keyword.cloud_notm}} の[前提条件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)トピックを参照してください。

<p>&nbsp;</p>

## ModelOps CLI ツール
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI モデル操作ツール](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}を使用すると、機械学習モデルのライフサイクル管理に関連するタスクを実行できます。 このツールは {{site.data.keyword.cloud_notm}} CLI ツールを補完するもので、[機械学習プラグイン](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}によって機能強化されます。

<p>&nbsp;</p>

## Python クライアント
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python クライアント](http://ai-openscale-python-client.mybluemix.net/){: external}は、{{site.data.keyword.cloud_notm}} 上で {{site.data.keyword.aios_short}} サービスを直接扱うことができる Python ライブラリーです。 {{site.data.keyword.aios_short}} クライアント UI ではなく Python クライアントを使用すると、ロギング・データベースの構成、機械学習エンジンのバインド、デプロイメントの選択とモニターを直接行うことができます。 例えば、このように Python クライアントを使用する場合には、[{{site.data.keyword.aios_short}} サンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)を参照してください。

<p>&nbsp;</p>

## 次のステップ
{: #in-next}

- サービスを[開始](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)します。
- [API リファレンス資料](https://{DomainName}/apidocs/ai-openscale){: external}を参照します。

まだご不明な点がありますか? 

- [新機能](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM にお問い合わせください](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
