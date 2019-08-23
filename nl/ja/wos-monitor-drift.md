---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# ドリフト検出モニターの構成 ![ベータ・タグ](images/beta.png)
{: #behavior-drift-config}

{{site.data.keyword.aios_full}} ドリフト・モニターでモデルの分析を開始する前に、ドリフト・モニターを構成する必要があります。 モデルをオンラインで訓練するかノートブックを使用するかという 2 つの選択肢があります。
{: shortdesc}

{{site.data.keyword.pm_full}} を使用し、データが 500 MB を超えない場合は、{{site.data.keyword.aios_short}} を使用してモデルをオンラインで訓練できます。 そうでない場合は、ノートブックを使用してモデルを訓練する必要があります。

## {{site.data.keyword.aios_short}} でドリフトを構成する手順
{: #behavior-drift-config-steps-wos}

{{site.data.keyword.pm_full}} を使用する場合は、{{site.data.keyword.aios_short}} ユーザー・インターフェースを使用してドリフト検出を構成することもできます。

1. **「ドリフト (Drift)」**タブの**「ドリフトとは (What is Drift?)」**ページで、**「開始」**をクリックして構成プロセスを開始します。

   ![「ドリフトとは (What is Drift?)」ページ](images/wos-drift-config-1.png)

2. **「Watson OpenScale で訓練 (Train in Watson OpenScale)」**タイルをクリックします。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-2.png)

3. 警告しきい値を設定します。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-3.png)

3. サンプル・サイズを設定します。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-4.png)
   
3. **「保存」**をクリックします。


## ノートブックを使用してドリフトを構成する手順
{: #behavior-drift-config-steps-ntbk}

{{site.data.keyword.pm_full}} 以外の機械学習プロバイダー (Microsoft Azure、Amazon SageMaker、カスタム機械学習エンジンなど) を使用する場合は、ノートブックを使用してドリフト検出を構成する必要があります。 この方法を使用して {{site.data.keyword.pm_full}} のドリフトを構成することもできます。

Db2 または {{site.data.keyword.cos_full}} に訓練データが保管されていない場合は、この方法が便利です。 ノートブックを使用して、訓練データをデータ・フレームに読み込む必要があります。 {{site.data.keyword.aios_short}} からダウンロードできる特別なノートブックを使用して、{{site.data.keyword.aios_short}} にアップロードできる特別な出力を作成します。

1. ノートブックを作成してドリフト検出モデルを生成します。 {{site.data.keyword.aios_short}} UI から使用可能な[サンプル・ノートブック](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb)を使用します。
2. 圧縮ソフトウェアを使用して、ドリフト検出モデルを .tar.gz ファイルとして圧縮します。

1. **「ドリフト (Drift)」**タブの**「ドリフトとは (What is Drift?)」**ページで、**「開始」**をクリックして構成プロセスを開始します。

   ![「ドリフトとは (What is Drift?)」ページ](images/wos-drift-config-1.png)

2. **「ノートブックで訓練 (Train in a notebook)」**タイルをクリックします。

   ![オンライン・オプションとノートブック・オプションが表示されているドリフト構成ページ](images/drift-config-2.png)

3. 圧縮モデル・ファイルをターゲット・ゾーンにドラッグするか参照して選択して、**「次へ」**をクリックします。

   ![「ドリフトとは (What is Drift?)」ページ](images/wos-drift-config-2b.png)
   
3. ドリフト検出モデルをアップロードし、**「次へ」**をクリックします。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-upload.png)
   
3. 警告しきい値を設定します。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-3.png)

3. サンプル・サイズを設定します。

   ![「ドリフトとは (What is Drift?)」ページ](images/drift-config-4.png)
   
3. **「保存」**をクリックします。

## 次のステップ
{: #behavior-drift-config-next-steps}

- ドリフトの解釈について詳しくは、[ドリフト絶対値](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)を参照してください。
