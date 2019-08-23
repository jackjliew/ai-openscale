---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# ペイロード・ロギングの自動化
{: #fmrk-workaround-pyld-lg}

同じ {{site.data.keyword.Bluemix_notm}} アカウントでプロビジョンした {{site.data.keyword.aios_full}} と {{site.data.keyword.pm_full}} の間では、自動ペイロード・ロギングが行われます。 また、以下のケースおよびオプションのいずれかを使用すれば、他の機械学習プロバイダーや、同じアカウントにない {{site.data.keyword.pm_full}} インスタンスのペイロード・ロギングも自動化できます。
{: shortdesc}

### ケース 1: 評価の入出力の元のフォーマット ({{site.data.keyword.aios_short}} で必要とされるものとは異なる) の保持
{: #fmrk-workaround-case1}

アプリケーションが、変更できない元のペイロード・フォーマットを使用する場合は、次のいずれかのオプションを選択します。

- オプション 1: カスタム機械学習エンジンの評価エンドポイントが、両方のペイロード・フォーマットを受け入れるようにします。 

   ペイロードのフォーマット ({{site.data.keyword.pm_full}} に似た {{site.data.keyword.aios_short}}、またはユーザーのフォーマット) に応じて、対応するフォーマットで出力を返します。 フォーマットがユーザーのフォーマットである場合は、{{site.data.keyword.aios_short}} のフォーマットに変換して、ペイロード・ロギング・テーブルのペイロード・レコードとして保管します。 評価入力フォーマットが {{site.data.keyword.aios_short}} のフォーマットである場合は、ペイロードを保管しないでください (このペイロードは、ユーザーからのものではなく {{site.data.keyword.aios_short}} からのものです)。

   詳しくは、[2 つのペイロード・フォーマットの使用](#fmrk-workaround-notsuppt)を参照してください。

- オプション 2: 何らかの理由で、そのようなロジックを単一の REST API エンドポイントに組み込むことができない場合は、2 つのエンドポイントを定義できます。 

   1 つは、アプリケーションによって使用されますが、ペイロード・ロギングを追加して、予期されるフォーマットに変換する必要があります。 2 つ目のエンドポイントは、{{site.data.keyword.aios_short}} によって、バイアスや説明性などの必要な計算を行うために使用されます。 このエンドポイントには、ペイロード・ロギングは必要ありません。 {{site.data.keyword.aios_short}} の構成中、2 つ目のエンドポイントが、準拠しているフォーマットのエンドポイントを指している必要があります。

   詳しくは、[2 つのエンドポイントの使用](#fmrk-workaround-opt2-cs1)を参照してください。

- オプション 3: ペイロード・ロギング・モジュールを元のエンドポイントまたはダウンストリーム・アプリケーションに移動します。 

   ご使用のアプリケーションがこのオプションをサポートしている場合は、カスタム機械学習エンジン上の 1 つのエンドポイントのみを開発するだけですみます。このエンドポイントは {{site.data.keyword.aios_short}} 用です。

### ケース 2: {{site.data.keyword.aios_short}} が必要とするペイロードのフォーマットの処理
{: #fmrk-workaround-case2}

このような場合は、ユーザーのフォーマット (評価入出力) から {{site.data.keyword.aios_short}} で必要とされるフォーマットへの変換を行う必要はありません。

内部評価要求は、ユーザー・ペイロードとしてログに記録する必要がありません ({{site.data.keyword.aios_short}} によって行われる計算であるため) 。そのため、2 つのエンドポイントを開発するか、単一のエンドポイントのための追加のロジックをコーディングする必要があります。

- オプション 1: 2 つのエンドポイント。 これは、ケース 1 のオプション 2 とほとんど同じです。唯一の違いは、2 つのフォーマットはすでに調整されているため、変換を行う必要がないことです。

- オプション 2: 単一のエンドポイント。 評価要求がユーザーのアプリケーションからのものかどうかを検出する必要があります。 これは、評価ペイロードでいくつかの追加の情報 (メタデータとも呼ばれる) を送信することで可能になります。 このようなメタデータが検出された場合は、ペイロードをログに記録する必要があります。

## 2 つのペイロード・フォーマットの使用
{: #fmrk-workaround-notsuppt}

XYZ オファリングを使用して、自分のモデルを提供しているとします。 XYZ は、この段階では {{site.data.keyword.aios_short}} でサポートされていません。

自分の多くのダウンストリーム・アプリケーションが XYZ の自分のデプロイメントを消費しており、評価ペイロードのフォーマットを変更することができません。 ただし、評価エンドポイントのロジックを変更できます。

### 手順

1. XYZ デプロイメントをラップするカスタム機械学習エンジンを開発します。
2. XYZ と {{site.data.keyword.aios_short}} の両方のペイロード・フォーマットをサポートできるように、カスタム機械学習エンジンに評価エンドポイントを実装します。
3. カスタム機械学習エンジンの評価エンドポイントに、ペイロードのフォーマットを検出するロジックを追加します。
4. ペイロードがダウンストリーム・アプリケーションから送信されたものである場合は、そのペイロードを {{site.data.keyword.aios_short}} フォーマットに変換して、{{site.data.keyword.aios_short}} のペイロード・レコードとしてログに記録します。
5. ダウンストリーム・アプリケーションの評価エンドポイントを、作成した新しい評価エンドポイントに切り替えます。

評価エンドポイントの URL を同じままにする必要がある場合は、プロキシーとも呼ばれる URL リダイレクトを使用します。

## 2 つのエンドポイントの使用
{: #fmrk-workaround-opt2-cs1}

ペイロードのフォーマットを変更することができない場合 (例えば、ダウンストリーム・アプリケーションが損なわれる場合) は、別個のエンドポイントを使用する必要があります。 この方法は、以下のコンポーネントから構成されます。

- 入出力の両方にユーザー定義フォーマットを使用する元の評価エンドポイントと (ユーザーのフォーマットの) 評価エンドポイント
- 摂動エンドポイント ({{site.data.keyword.aios_short}} フォーマット) およびディスカバリー・エンドポイントを使用するカスタム ML エンジン。 摂動エンドポイントでは、元の評価エンドポイントがラップされて、{{site.data.keyword.aios_short}} フォーマットからユーザーのフォーマットへの変換、およびユーザーの出力から {{site.data.keyword.aios_short}} の出力への変換が行われます。 これは、{{site.data.keyword.aios_short}} で、正しい評価要求を行い、出力を認識するために必要です。
- ペイロード・ロギング機能を備えた評価エンドポイント・ラッパー。 このラッパーは、元の評価エンドポイントではなく、ダウンストリーム・アプリケーションによって消費されます。 ペイロード・ロギング機能によって、このロジックが拡張されています。 評価要求が実行されるたびに、入出力が {{site.data.keyword.aios_short}} フォーマットに変換されて、ログに記録されます。

以下のフローチャートは、カスタム機械学習エンジンが摂動エンドポイントとディスカバリー・エンドポイントを処理してユーザーのフォーマットに変換する、カスタム機械学習エンジンのソリューションを示しています。

![REST API エンドポイント仕様](images/woscustommlworkflow.png)

### 手順
{: #fmrk-workaround-smple-cd}

1. ノートブックを使用して、Microsoft Azure Machine Learning Service で、信用リスク・モデル (scikit-learn) デプロイメントの評価エンドポイントを作成します。 詳しくは、[このサンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb)を参照してください。
2. カスタム機械学習エンジンを作成して、Microsoft Azure Cloud に Flask アプリケーションとしてデプロイします。 摂動エンドポイントとディスカバリー・エンドポイントを作成します。詳しくは、[これらのデプロイメント手順](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure)を参照してください。
3. {{site.data.keyword.aios_short}} を、カスタム機械学習エンジンと連動するように構成します。詳しくは、[このサンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb)を参照してください。
4. Microsoft Azure Machine Learning Service でペイロード・ロギングを自動化する評価エンドポイント・ラッパーを作成します。 詳しくは、[このサンプル・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb)を参照してください。

以下の項目に特に注意してください。

- 資格情報: チュートリアルをより行いやすくするために、{{site.data.keyword.aios_short}} 資格情報がコード (評価エンドポイント・ラッパー) 内にハードコーディングされています。 これらの値を実際の資格情報に更新する必要があります。
- Python SDK と REST API: チュートリアルでは、Python SDK を使用してペイロードをログに記録します。 REST API を使用してこれを行うこともできますが、ユーザー自身でトークンを生成またはリフレッシュする必要があります。 
- {{site.data.keyword.cloud_notm}} と Cloud Pak for Data: {{site.data.keyword.wos4d_notm}} を使用している場合、資格情報のフォーマットは異なります ([ここにサンプル・ノートブックを示します](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb))。 {{site.data.keyword.aios_short}} クライアント・クラスも異なります。 この場合、`APIClient4ICP` クライアント・クラスが使用されます。
- 別個のパッケージ/エンドポイントとしてのペイロード・ロギング — パッケージまたはエンドポイントを分離するペイロード・ロギングの抽出と変換の方法。 この方法を使用すると、評価エンドポイント・ラッパーの外側でペイロードのバッチを注入する場合に、ペイロード・ロギングを再利用できます。

