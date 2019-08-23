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

# バイアス緩和のオプション
{: #it-dbo}

{{site.data.keyword.aios_short}} では 2 種類のバイアス緩和を使用します。受動的なものとアクティブなものです。受動的なバイアス緩和では、バイアスが存在していた状況がユーザーに知らされます。一方、アクティブなバイアス緩和では、リアルタイムでモデルを変更して、現行のアプリケーションにそのバイアスが渡らないようにします。

- *受動的なバイアス緩和* - 受動的なバイアス緩和は、OpenScale 自体が、自動で 1 時間おきに実行する処理です。「受動的」というのは、ユーザー介入なしで実行されるからです。{{site.data.keyword.aios_short}} は、バイアス検査の実行と同時に、モデルの動作を分析し、モデルがバイアス挙動を示すデータを特定することで、データのバイアス緩和も実行します。

  {{site.data.keyword.aios_short}} は次に、特定の新しいデータ・ポイントでモデルがバイアス挙動を示す可能性が高いかどうかを予測するための機械学習モデルを構築します。 その後、{{site.data.keyword.aios_short}} はモデルで受け取ったデータを 1 時間ごとに分析し、モデルがバイアス挙動を示すと {{site.data.keyword.aios_short}} が判断したデータ・ポイントを検出します。 こうしたデータ・ポイントでは、公平性属性は少数派から多数派に摂動され、摂動されたデータが元のモデルに送られて予測が行われます。 この元のモデルの予測がバイアス緩和出力として使用されます。

  {{site.data.keyword.aios_short}} はこのバイアス緩和を、過去 1 時間にモデルで受け取ったすべてのデータに対して 1 時間ごとに実行します。 また、バイアス緩和された出力の公平性を計算し、それを**「バイアスが緩和されたモデル」**タブに表示します。

- *アクティブなバイアス緩和* - アクティブなバイアス緩和とは、ユーザーが REST API エンドポイントを使用してバイアス緩和を要求し、バイアス緩和済みの結果をアプリケーションに返す手段です。バイアスのない状態でアプリケーションを実行できるように、ユーザーが積極的に {{site.data.keyword.aios_short}} にバイアス緩和の実行を指示し、モデルを変更します。アクティブなバイアス緩和では、アプリケーションからバイアス緩和 REST API エンドポイントを利用できます。この REST API エンドポイントは内部でモデルを呼び出し、その振る舞いを検査します。

  {{site.data.keyword.aios_short}} で、モデルがバイアスのある状態で動作していると検出された場合、前述のようにデータを摂動して、それが元のモデルに返送されます。 摂動されたデータに対する元のモデルの出力は、バイアス緩和した予測として返されます。 元のモデルがバイアス挙動を示していないと {{site.data.keyword.aios_short}} が判断すると、{{site.data.keyword.aios_short}} はバイアス緩和予測として元のモデルの予測を返します。 したがって、この REST API エンドポイントを使用することにより、アプリケーションがモデルのバイアス出力に基づいて決定を行うことを防止できます。

バイアス緩和 REST API エンドポイントを検出するには、**「バイアスが排除された予測エンドポイント」**リンクを選択します。

![バイアス緩和 API エンドポイント詳細画面のコード・スニペット・ボックスに、cURL の例が表示されています。](images/insight-debias-api.png)

## 次のステップ
{: #it-dbo-nextsteps}

- バイアスの検出後にバイアスを緩和するには、その問題を修正する新しいバージョンのモデルを作成する必要があります。{{site.data.keyword.aios_short}} は、バイアスのあるレコードを手動ラベル付けテーブルに保管します。このようなバイアスのあるレコードには手動でラベルを付ける必要があります。その後、バイアスのないモデルの新しいバージョンを作成するため、この追加データを使用してモデルを再訓練する必要があります。


