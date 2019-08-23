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

# デプロイメントのデータの表示
{: #it-vdep}

ダッシュボードからデプロイメントを選択し、そのデプロイメントのモニタリング・データを確認します。 **「モデル ID」**フィールドや**「作成日 (Created date)」**フィールドなど、デプロイ済みモデルに関する情報が見出しに表示されます。
{: shortdesc}

![時系列グラフに 1 日の時間と公平性スコアが表示されています](images/insight-time-chart.png)

アルゴリズム・チェックは 1 時間おきにしか実行されないので、公平性とモデル性能をオンデマンドで評価するためのリンクも用意されています。 **「スケジュール」**パネルから以下のリンクをクリックすると、データをすぐに評価できます。

![公平性の評価ボタンが表示されています](images/wos-fairness-button.png)


![品質の評価ボタンが表示されています](images/wos-quality-button.png)

次に、グラフをクリックし、グラフ上でマーカーを動かし、特定の時間の統計を表示します。

![時系列グラフの詳細、グラフで選択されている特定のデータ・ポイント、クリックすると詳細が表示されることを示すツールチップが表示されています。](images/wos-insight-time-detail.png)

- ***公平性***: 2 つの公平性特徴量 (Sex と Age) が、承認のしきい値設定を満たしています。
- ***モデル性能***: 構成されたしきい値を超えていたため、**ROC 曲線下面積**指標に警告が表示されています。
- ***平均要求数/分***: **「スループット」**指標をクリックすると、1 分間に処理されたレコードの数が表示されます。 このスループットは毎分計算され、グラフには 1 時間の平均値が報告されます。


## トランザクションの表示
{: #it-tra}

このオプションでは、**「トランザクションの表示」**ボタンをクリックすると、バイアスの原因となった個々のトランザクションを表示できます。

![トランザクションの表示ボタンが表示されています](images/view_transactions.png)

デプロイメントがバイアス挙動を示すトランザクションがリストされます。 任意のトランザクション ID の**「説明」**リンクをクリックすると、「説明性」タブにそのトランザクションに関する詳細が示されます。 詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

選択した特徴量 (この例では「AGE」) および選択した期間 (この例では「September 15, 2018 1:00 PM」) のすべてのトランザクションを表示するには、**「すべてのトランザクション」**ビューを選択します。

![「トランザクション」に特定データ・ポイントのすべてのトランザクションがリストされています](images/transaction_list1.png)

バイアスありの結果となったトランザクションのサブセットのみを表示するには、**「バイアスのあるトランザクション」**ビューを選択します。 バイアスのある各トランザクションは、類似しているがわずかに変更された (摂動された) トランザクションと比較されます。これにより、モニター対象の特徴量 (AGE) の値を変更することで、バイアスのあるトランザクションがどのように好ましい結果になるかが示されます。

![「トランザクション」にバイアスのあるトランザクションだけがリストされています](images/transaction_list2.png)


