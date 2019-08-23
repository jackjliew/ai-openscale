---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

{{site.data.keyword.pm_full}} を使用して、ペイロード・ロギングとフィードバック・ロギングを実行し、{{site.data.keyword.aios_full}} でパフォーマンスの正確度、実行時のバイアス検出、説明性、および自動バイアス緩和機能を測定することができます。

{{site.data.keyword.aios_full}} では以下の {{site.data.keyword.pm_full}} フレームワークが完全にサポートされています。 
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| Apache Spark MLlib | 分類 | 構造化 |
| Apache Spark MLLib | 回帰 | 構造化 |
| Keras と TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | 分類 | 非構造化 (イメージ、テキスト) |
| Keras と TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | 回帰 | 非構造化 (イメージ、テキスト) |
| Python 関数 | 分類 | 構造化 |
| Python 関数 | 回帰 | 構造化 |
| scikit-learn | 分類 | 構造化 |
| scikit-learn | 回帰 | 構造化 |
| XGBoost | 分類 | 構造化 |
| XGBoost | 回帰 | 構造化 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

<sup>1</sup>Keras のサポートには、公平性のサポートは含まれていません。
{: note}

<sup>2</sup> 説明性は、モデル/フレームワークが予測確率を出力する場合にサポートされています。
{: note}

## {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} サービス・インスタンスの指定
{: #wml-connect}

{{site.data.keyword.aios_short}} ツールで最初に実行するステップは、{{site.data.keyword.pm_full}} インスタンスの指定です。 {{site.data.keyword.pm_short}} インスタンスは、AI モデルとデプロイメントの格納場所となります。
{: shortdesc}

### 前提条件
{: #wml-prereq}

{{site.data.keyword.pm_full}} インスタンスを、{{site.data.keyword.aios_short}} サービス・インスタンスが配置されている {{site.data.keyword.Bluemix_notm}} アカウントと同じアカウントでプロビジョンしておく必要があります。 他のアカウントで {{site.data.keyword.pm_full}} インスタンスをプロビジョンした場合、そのインスタンスには {{site.data.keyword.aios_short}} の自動ペイロード・ロギングは構成できません。

### {{site.data.keyword.pm_short}} サービス・インスタンスの接続
{: #wml-config}

{{site.data.keyword.aios_short}} は、{{site.data.keyword.pm_full}} インスタンス内の AI モデルとデプロイメントに接続します。

1.  ナビゲーション・ペインの**「構成」**タブで**「機械学習プロバイダー (Machine learning providers)」**をクリックします。

    ![機械学習サービス・プロバイダーの選択画面に、サポートされる機械学習エンジンのタイルが表示されます](images/wos-machine-learning-providers-selection.png)

2.  **「機械学習プロバイダーの追加 (Add machine learning provider)」**ボタンをクリックし、「{{site.data.keyword.pm_full}}」タイルをクリックします。{{site.data.keyword.aios_short}} によって {{site.data.keyword.Bluemix_notm}} アカウントが調べられ、既存の {{site.data.keyword.pm_full}} インスタンスが検出されます。 
3. **「Watson Machine Learning service」**ドロップダウン・メニューからインスタンスを選択します。

    ![{{site.data.keyword.pm_short}} サービスの選択](images/gs-set-wml.png)

4.  (オプション)**「別の場所を選択」**を選択し、ご使用の {{site.data.keyword.Bluemix_notm}} アカウント以外の機械学習の場所を指定することもできます。 ご使用の場所の資格情報を有効な JSON として指定します。

    ![{{site.data.keyword.pm_short}} インスタンスの設定](images/gs-get-wml.png)

    **「保存」**をクリックします。

1.  デプロイされているモデルのリストが {{site.data.keyword.aios_short}} に表示されるので、モニターするモデルを選択して**「構成」**をクリックします。

## 次のステップ
{: #wml-next}

{{site.data.keyword.aios_short}} で、[モニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。
