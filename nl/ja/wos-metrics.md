---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# カスタム・モニターとカスタム指標の作成 ![ベータ・タグ](images/beta.png)
{: #cst_mtrcs}

カスタム・モニターが統合しているカスタム指標のセットを使用すると、モデル・デプロイメントとビジネス・アプリケーションのあらゆる面を定量的に追跡できます。 カスタム指標を定義して、標準的な指標 ({{site.data.keyword.aios_full}} でモニターされるモデルの品質、パフォーマンス、公平性の指標など) と併用できます。
{: shortdesc}

カスタム・モニターとカスタム指標を管理するには、Python SDK の一部であるプログラマチック・インターフェースを使用する必要があります。 同様に、カスタム指標を {{site.data.keyword.aios_short}} データマートに格納しておいて、必要なときにアクセスできます。 カスタム指標は、{{site.data.keyword.aios_short}} ダッシュボードでも視覚化されます。

## カスタム指標の管理
{: #cst_mtrc_mgmt}

カスタム指標を処理するには、以下のタスクを実行する必要があります。

1. カスタム・モニターを指標定義に登録します。
2. カスタム・モニターを有効にします。
3. 指標値を格納します。

その方法については、次のアドバンスト・チュートリアルを参照してください。

- [{{site.data.keyword.pm_full}} での作業](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

カスタム・モニターはいつでも無効にでき、また再び有効にすることもできます。 不要になったカスタム・モニターは削除できます。

詳しくは、[Python SDK の資料](http://ai-openscale-python-client.mybluemix.net/)を参照してください。

## カスタム指標へのアクセスとその視覚化
{: #cst_mtrcs_viz}

カスタム指標にアクセスして視覚化するには、プログラマチック・インターフェースを使用できます。 その方法については、次のアドバンスト・チュートリアルを参照してください。

- [{{site.data.keyword.pm_full}} での作業](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Working with Custom Machine Learning engine](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   詳しくは、[Python SDK の資料](http://ai-openscale-python-client.mybluemix.net/)を参照してください。

カスタム指標を視覚化すると、{{site.data.keyword.aios_short}} ダッシュボード上で表示されます。

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
