---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# FAQ
{: #wos-faqs}

{{site.data.keyword.aios_full}} ユーザーからよく尋ねられる質問の一部を以下に示します。
{: shortdesc}

## 質問
{: #wos-faqs-questions}

- [{{site.data.keyword.aios_short}} とは何ですか?](#faq-whatsa)
- [{{site.data.keyword.aios_short}} の価格はどのように設定されていますか?](#faq-pricing)
- [{{site.data.keyword.aios_short}} の無料試用版はありますか?](#faq-freetrial)
- [私の AI モデルはすべて Azure にあります。 {{site.data.keyword.aios_short}} で Microsoft Azure ML エンジンを使用することはできますか?](#faq-azure)
- [私の AI モデルはすべて Amazon にあります。 {{site.data.keyword.aios_short}} で Amazon SageMaker ML エンジンを使用することはできますか?](#faq-sagemaker)
- [{{site.data.keyword.aios_short}} は {{site.data.keyword.icp4dfull_notm}} で使用できますか?](#faq-icp)
- [{{site.data.keyword.aios_short}} 自分のサーバーで実行したいと思っています。 コンピューターの処理能力はどれくらい割り当てる必要がありますか?](#faq-sizing)
- [整数データ型の予測列をカテゴリカル・データ型にどのように変換できますか?](#wos-faqs-convert-data-types)
- [{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](#trainingdata)

### {{site.data.keyword.aios_short}} とは何ですか?
{: #faq-whatsa}

Watson OpenScale を使用すると、AI の結果をライフサイクルを通して追跡および測定し、ビジネス状況の変化に合わせて AI を適応させ、管理することができます。実行場所にかかわらず、作成済みのモデルに使用できます。

{{site.data.keyword.aios_short}} の概要は、以下の動画を見て確認してください。

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Trust and Transparency in AI" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### {{site.data.keyword.aios_short}} の価格はどのように設定されていますか?
{: #faq-pricing}

ライト・プランから移行する準備ができたら、**「Standard」**の価格設定プランがあります。このプランでは、最大 24 個のデプロイ済みモデルをモニターできます。説明性に関するペイロード数、フィードバック行数、トランザクション数の制限はありません。 最新の情報については、[{{site.data.keyword.Bluemix}} カタログ](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external}を参照してください。


### {{site.data.keyword.aios_short}} の無料試用版はありますか?
{: #faq-freetrial}

{{site.data.keyword.aios_short}} には、ライト・プランの無料試用版が用意されています。 登録するには、[{{site.data.keyword.aios_short}} Web ページ](https://www.ibm.com/cloud/watson-openscale/){: external}にアクセスして、**「Get started now」**をクリックします。 ライト・プランの使用期間は無制限です (毎月リフレッシュされる月単位の使用量制限はあります)。

### 私の AI モデルはすべて Azure にあります。 {{site.data.keyword.aios_short}} で Microsoft Azure ML エンジンを使用することはできますか?
{: #faq-azure}

{{site.data.keyword.aios_short}} は、Microsoft Azure ML Studio エンジンと Microsoft Azure ML Service エンジンの両方をサポートしています。 詳しくは、[Microsoft Azure ML Studio フレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure)および [Microsoft Azure ML Service フレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)を参照してください。

### 私の AI モデルはすべて Amazon にあります。 {{site.data.keyword.aios_short}} で Amazon SageMaker ML エンジンを使用することはできますか?
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} は Amazon SageMaker ML エンジンをサポートしています。 詳しくは、[Amazon SageMaker フレームワーク](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage)を参照してください。

### {{site.data.keyword.aios_short}} は {{site.data.keyword.icp4dfull_notm}} で使用できますか?
{: #faq-icp}

{{site.data.keyword.aios_short}} は {{site.data.keyword.icp4dfull_notm}} のプレミアム・アドオンの 1 つです。 

### 自分のサーバーで {{site.data.keyword.aios_short}} を実行したいと思っています。 コンピューターの処理能力はどれくらい割り当てる必要がありますか?
{: #faq-sizing}

3 ノード構成および 6 ノード構成については、固有の[ハードウェア構成](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt)ガイドラインがあります。 具体的な構成のサイズ設定について、IBM の技術販売チームから支援を受けることもできます。 {{site.data.keyword.aios_short}} は {{site.data.keyword.icp4dfull_notm}} のアドオンとして実行されるので、この両方のソフトウェア製品の要件を検討する必要があります。

### 整数データ型の予測列をカテゴリカル・データ型にどのように変換できますか?
{: #wos-faqs-convert-data-types}

モデルの公平性モニターを構成する際、予測ラベルがカテゴリカルであっても予測列で使用できるのは整数値のみです。整数値ではないカテゴリーの特徴量を使用するにはどのように構成すればよいですか。手動で変換することが必要ですか? 

訓練データには「Loan Denied」、「Loan Granted」などのクラス・ラベルを含めることができます。 {{site.data.keyword.pm_full}} 評価エンドポイントが返す予測値は、「0.0」、「1.0」などの値です。また、評価エンドポイントには、予測のテキスト表現を入れるオプション列もあります。 例えば、予測 = 1.0 の場合、predictionLabel 列に「Loan Granted」という値を入れることができます。 そのような列がある場合、モデルに好ましい結果と好ましくない結果を構成するときに、ストリング値として「Loan Granted」と「Loan Denied」を指定することができます。 こうした列がない場合には、好ましい/好ましくないクラスに関して整数/倍精度値の 1.0、0.0 を指定する必要があります。

{{site.data.keyword.pm_full}} には出力スキーマの概念があり、{{site.data.keyword.pm_full}} 評価エンドポイントの出力のスキーマと、さまざまな列のロールを定義できます。 ロールは、予測値を入れる列、予測の確率を入れる列、クラス・ラベル値などを指定するために使用します。出力スキーマは、モデル・ビルダーを使用して作成されたモデルに関しては自動的に設定されます。 これは、{{site.data.keyword.pm_full}} Python クライアントを使用して設定することもできます。 ユーザーは、出力スキーマを使用して予測のストリング表現を入れる列を定義できます。 その場合には、列の modeling_role を「decoded-target」に設定します。 {{site.data.keyword.pm_full}} Python クライアントの資料は、http://wml-api-pyclient-dev.mybluemix.net/#repository から参照できます。 「OUTPUT_DATA_SCHEMA」を検索して、出力スキーマと、パラメーターとして OUTPUT_DATA_SCHEMA を受け入れる store_model メソッドについての理解を深めてください。

### {{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?
{: #trainingdata}

Db2 または {{site.data.keyword.cos_full_notm}} に格納されている訓練データへのアクセス権限を {{site.data.keyword.aios_short}} に提供するか、または訓練データにアクセスできるノートブックを実行する必要があります。 以下の理由で、{{site.data.keyword.aios_short}} は訓練データにアクセスする必要があります。

- 対比的説明を生成するため。説明を作成するには、訓練データの統計 (中央値、標準偏差、個別の値など) に対するアクセス権限が必要です。
- 訓練データの統計を表示するため。 バイアスの詳細ページにデータを取り込むために、{{site.data.keyword.aios_short}} は統計を生成する基になる訓練データを必要とします。

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

ノートブック・ベースの方法では、{{site.data.keyword.aios_short}} でデプロイメントを構成する際に統計およびその他の情報をアップロードすることが求められます。 こうすることは、環境で実行されているノートブック以外の訓練データには、{{site.data.keyword.aios_short}} がアクセスできなくなることを意味します。 構成中にアップロードされた情報にのみアクセスできることになります。


