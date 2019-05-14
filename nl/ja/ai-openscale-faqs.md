---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: FAQs, frequently asked questions, questions

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

# FAQ
{: #wos-faqs}

{{site.data.keyword.aios_full}} ユーザーからよく尋ねられる質問の一部を以下に示します。
{: shortdesc}

## 質問
{: #wos-faqs-questions}

- [整数データ型の予測列をカテゴリカル・データ型にどのように変換できますか?](#wos-faqs-convert-data-types)

### 整数データ型の予測列をカテゴリカル・データ型にどのように変換できますか?
{: #wos-faqs-convert-data-types}

モデルの公平性モニターを構成する際、予測ラベルがカテゴリカルであっても予測列で使用できるのは整数値のみです。整数値ではないカテゴリー項目を使用するにはどのように構成すればよいですか。手動で変換することが必要ですか? 

トレーニング・データには「Loan Denied」、「Loan Granted」などのクラス・ラベルを含めることができます。WML 予測エンドポイントが返す予測値は、「0.0」、「1.0」などの値です。また、予測エンドポイントには、予測のテキスト表現を入れるオプション列もあります。例えば、予測 = 1.0 の場合、predictionLabel 列に「Loan Granted」という値を入れることができます。そのような列がある場合、モデルに好ましい結果と好ましくない結果を構成するときに、ストリング値として「Loan Granted」と「Loan Denied」を指定することができます。こうした列がない場合には、好ましい/好ましくないクラスに関して整数/倍精度値の 1.0、0.0 を指定する必要があります。

WML には出力スキーマの概念があり、WML 予測エンドポイントの出力のスキーマと、さまざまな列のロールを定義できます。ロールは、予測値を入れる列、予測の確率を入れる列、クラス・ラベル値などを指定するために使用します。出力スキーマは、モデル・ビルダーを使用して作成されたモデルに関しては自動的に設定されます。これは、WML Python クライアントを使用して設定することもできます。ユーザーは、出力スキーマを使用して予測のストリング表現を入れる列を定義できます。その場合には、列の modeling_role を「decoded-target」に設定します。WML Python クライアントの資料は、http://wml-api-pyclient-dev.mybluemix.net/#repository から参照できます。「OUTPUT_DATA_SCHEMA」を検索して、出力スキーマと、パラメーターとして OUTPUT_DATA_SCHEMA を受け入れる store_model メソッドについての理解を深めてください。



