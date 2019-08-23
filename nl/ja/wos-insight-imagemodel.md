---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 画像モデルの説明
{: #ie-image}

{{site.data.keyword.aios_short}} は、画像データの説明性をサポートします。
{: shortdesc}

## 画像モデルの処理
{: #ie-image-working}

1. 環境をセットアップします。
   2. {{site.data.keyword.aios_short}} パッケージと {{site.data.keyword.pm_full}} パッケージをインストールします。
   3. 資格情報を構成します。
   4. モデルの作成や分析に必要なライブラリーをインストールします。これには、次のライブラリーが含まれます。
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. 画像ベースのモデルを作成してデプロイします。
   2. 画像の分類に基づいて、画像用のフォルダーを作成します。
       - メインの `data` ディレクトリー内に、`train` と `validation` の各サブディレクトリーを作成する必要があります。
       - 各サブディレクトリー内に、独自の分類ディレクトリーを作成する必要があります。
  2. 画像のサイズを標準化し、訓練用と検証用に使用するサブディレクトリーを設定します。
  3. データを前処理してスケールを変更し、画像とそのクラスを取り出します。
  4. モデルを定義し、訓練を行います。
  5. モデルを保管します。
  6. モデルをデプロイします。

7. `APIClient` を割り当て、アセットをサブスクライブし、モデルを評価することで、{{site.data.keyword.aios_short}} を構成します。
8. 説明性を構成します。
   9. 説明性を有効にします。
   10. トランザクションの説明性を取得します。
   11. 説明された画像を表示します。 

## 画像モデルのトランザクションの説明
{: #ie-image-workingviewing}

説明性の例が画像分類モデルである場合、画像のどの部分が予測結果のプラス要因となり、どの部分がマイナス要因となったのかを確認できます。 以下の例では、プラスのペインのイメージは予測にプラスに影響した部分を示し、マイナスのペインのイメージは結果にマイナスの影響があった部分を示しています。

![説明性画像分類の確信度の詳細に、犬の画像が表示されており、この画像の一部は、犬の画像であると判断する上で役に立った画像の部分であることを示すため強調表示されています](images/insight-explain-image.png)

{{site.data.keyword.pm_full}} では、ペイロード・ロギングのために送信する画像分類モデルの評価入力データは、(ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service) MB を超えてはなりません。タイムアウトの問題を避けるには、イメージは 125 x 125 ピクセルを超えてはならず、最初のものが完了してから 2 番目のイメージの説明が要求されるように、順次送信される必要があります。
{: note}


## 画像モデルの例
{: #ie-image-working-ntbks}

次の 2 つのノートブックを使用して、詳細なコードの例を確認し、独自の {{site.data.keyword.aios_short}} デプロイメントを開発してください。

- [画像ベース・モデルの説明を生成するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [画像ベース 2 項分類器モデルの説明の生成に関するチュートリアル](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

