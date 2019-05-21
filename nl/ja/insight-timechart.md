---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 公平性、毎分平均リクエスト数、正解率のモニター
{: #it-ov}

個々のデプロイメントのモニタリング・データは、時系列グラフに表示されます。グラフは、過去 7 日間の公平性、毎分平均リクエスト数、正解率を追跡します。
{: shortdesc}

## デプロイメントのデータの表示
{: #it-vdep}

ダッシュボードからデプロイメントを選択し、そのデプロイメントのモニタリング・データを確認します。モニタリング・データのグラフの上部には、デプロイ済みモデルに関する情報が表示されます。これにはモデルの公平性と正解率が最後に評価された時刻と、次回に評価される時刻も含まれます。

![時系列グラフ](images/insight-time-chart.png)

アルゴリズム・チェックは 1 時間おきにしか実行されないので、公平性と正解率をオンデマンドで確認できるボタンも用意されています。十分なペイロード・レコード (公平性) やフィードバック・レコード (正解率) が提供されていない場合、例として以下のようなメッセージが表示されます。

![正解率ボタン](images/accuracy-button.png)

次に、グラフの上でマーカーを移動して、特定の時間の統計を確認します。この例では、選択された時刻は 9 月 18 日の午後 1:00 (CST) で、以下の統計が明らかになります。

![時系列グラフの詳細](images/insight-time-detail.png)

- ***公平性***: 3 つの公平性項目のうち、「Car Value」と「Area Code」の 2 つが、承認のために設定したしきい値を満たしました。3 つ目の公平性項目である「Age」には、バイアス・フラグが付いています。また、公平性のモニター対象となる各項目の個々の母数の予測される結果の数 (このケースでは「Approved」と「Denied」の割合) も確認できます。
- ***正解率***: 正解率メトリックの平均は 78% でした。
- ***平均リクエスト数/分***: 午後 1:00 から 2:00 (CST) に処理されたレコードは、平均 300 レコード/分でした。このスループットは毎分計算され、グラフには 1 時間の平均値が報告されます。

## 特定の時間のデータの視覚化
{: #it-vdet}

個々の公平性統計の背景となる詳細を調べるには、選択した時間の**「詳細を表示します」**リンクをクリックします。

モニター対象項目における選択した時間のデータ・ポイントの視覚化が開きます。前の例で言及したバイアスのタグが付いた「Age」項目が表示されます。

ページの上部に 3 つのフィルター (項目、日付、時間) があり、詳細を確認するために異なる項目や時刻を選択できることに注目してください。

![時系列グラフ](images/insight-data-detail.png)

### グラフの解釈
{: #it-intp}

グラフからはさまざまな事柄が分かります。

- バイアスが発生している集団 (18 歳から 23 歳の顧客) を観察できます。グラフは、この集団の予想結果の割合 (52%) も示しています。

- グラフは、参照集団の予想結果の割合 (70%) を示しています。これは、すべての参照集団に対する予想結果の平均です。

- グラフは、バイアスがあることを示しています。参照集団の予想結果の割合を基準とする年齢 18 歳から 23 歳の集団の予想結果の割合の比率が、しきい値を下回っているからです。つまり、0.52/0.7 = 0.74 であり、しきい値 0.8 より小さい値となっています。

- グラフは、ペイロード・テーブルのデータにある属性の個別の各値 (バイアスを識別するために分析された値) について、参照値とモニター対象値の分布も示しています。つまり、バイアス検出アルゴリズムがペイロード・テーブルの最後の 1790 件のレコードを分析した場合、それらのレコードのうち 120 件は顧客の年齢が 18 歳から 23 歳であり、その分布のうち `Approved` と `Denied` の結果が棒グラフで表示されます。公平性属性の個別の値ごとに、ペイロード・データの分布が示されます (参照値も表示されます)。この情報を使用して、モデルから受け取ったデータ量にバイアスを相関させることができます。

- グラフはさらに、年齢が 31 歳から 35 歳の集団が 91% の予想結果になっていることを示しています。これは、バイアスのソースを意味しています。つまり、このグループのデータが結果をゆがませ、参照クラスにおける予想結果の割合の増加につながったことを意味します。この情報を使用して、モデルをリトレーニングする際にデータのどの部分がサンプル不足となる可能性があるかを特定できます。

- グラフで示される別の重要な事項は、手動ラベル付けのために識別されたデータが含まれるテーブルの名前です。アルゴリズムがモデルでバイアスを検出する際は常に、人間が手動でラベル付けするために送信できるデータ・ポイントも特定します。この手動でラベル付けされるデータを、元のトレーニング・データとともに使用してモデルをリトレーニングできます。このリトレーニングされたモデルには、バイアスがない可能性が高くなります。手動ラベリング・テーブルは、{{site.data.keyword.aios_short}} インスタンスに関連付けられたデータベースにあります。

## 実行時データとトレーニング・データ
{: #it-rtsw}

「実行時データ」と「トレーニング・データ」のスイッチによって、トレーニングされたモデルと、実行時に収集されたデータ (バイアス警告をトリガーしているデータ) の間で切り替えることができます。

![実行時とトレーニングの切り替え](images/runtime_train_data.png)

## トランザクションの表示
{: #it-tra}

このオプションでは、**「トランザクションの表示」**ボタンをクリックすると、バイアスの原因となった個々のトランザクションを表示できます。

![トランザクションの表示](images/view_transactions.png)

デプロイメントがバイアス挙動を示すトランザクションがリストされます。任意のトランザクション ID の**「説明」**リンクをクリックすると、「説明性」タブにそのトランザクションに関する詳細が示されます。詳しくは、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。

選択した項目 (この例では「AGE」) および選択した期間 (この例では「September 15, 2018 1:00 PM」) のすべてのトランザクションを表示するには、**「すべてのトランザクション」**ビューを選択します。

![すべてのトランザクションのリスト](images/transaction_list1.png)

バイアスありの結果となったトランザクションのサブセットのみを表示するには、**「バイアスのあるトランザクション」**ビューを選択します。バイアスのある各トランザクションは、類似しているがわずかに変更された (摂動された) トランザクションと比較されます。これにより、モニター対象の項目 (AGE) の値を変更することで、バイアスのあるトランザクションがどのように好ましい結果になるかが示されます。

![バイアスのあるトランザクションのリスト](images/transaction_list2.png)

## 実動モデルとバイアスが排除されたモデル
{: #it-prdb}

これらの 2 つのタブを使用して、{{site.data.keyword.aios_short}} で作成されたバイアスが排除されたモデルと実動モデルの間で切り替えることができます。詳しくは、[バイアス緩和の処理の流れについて](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)を参照してください。

![実行時とトレーニングの切り替え](images/bias-debias.png)

**「バイアスが排除されたモデル」**タブを選択すると、実動のモデルと比較した場合の、バイアスが排除されたモデルの変更点が表示されます。この例では、モデルの公平性が 74% から 93% に増えた一方で、正解率はわずか 1% 下がっただけです。グラフには、年齢が 18 歳から 23 歳のグループの改善された結果状況も反映されます。

![実行時とトレーニングの切り替え](images/insight-data-detail2.png)

### バイアス緩和のオプション
{: #it-dbo}

- *受動的なバイアス緩和* - {{site.data.keyword.aios_short}} がバイアス・チェックを行う際に、モデルの動作を分析し、モデルがバイアス挙動を示すデータを特定することにより、データのバイアス緩和も行います。

  {{site.data.keyword.aios_short}} は次に、所定の新しいデータ・ポイントでモデルがバイアス挙動を示す可能性が高いかどうかを予測するための機械学習モデルを構築します。その後、{{site.data.keyword.aios_short}} はモデルで受け取ったデータを 1 時間ごとに分析し、モデルがバイアス挙動を示すと {{site.data.keyword.aios_short}} が考えるデータ・ポイントを検出します。こうしたデータ・ポイントでは、公平性属性は少数派から多数派に摂動され、摂動されたデータが元のモデルに送られて予測が行われます。この元のモデルの予測がバイアス緩和出力として使用されます。

  {{site.data.keyword.aios_short}} はこのバイアス緩和を、過去 1 時間にモデルで受け取ったすべてのデータに対して 1 時間ごとに実行します。また、バイアス緩和された出力の公平性を計算し、それを**「バイアスが排除されたモデル」**タブに表示します。

- *アクティブなバイアス緩和* - アクティブなバイアス緩和では、アプリケーションのバイアス緩和 REST API エンドポイントを利用できます。この REST API エンドポイントは内部でモデルを呼び出し、その振る舞いを検査します。

  モデルがバイアス挙動を示していると {{site.data.keyword.aios_short}} が判断すると、上述のようにデータの摂動を行い、それを元のモデルに返送します。摂動されたデータに対する元のモデルの出力は、バイアス緩和した予測として返されます。元のモデルがバイアス挙動を示していないと {{site.data.keyword.aios_short}} が判断すると、{{site.data.keyword.aios_short}} はバイアス緩和予測として元のモデルの予測を返します。したがって、この REST API エンドポイントを使用することにより、アプリケーションがモデルのバイアス出力に基づいて決定を行なうことを防止できます。

バイアス緩和 REST API エンドポイントを検出するには、**「バイアスが排除された予測エンドポイント」**リンクを選択します

![バイアス緩和 API エンドポイント](images/insight-debias-api.png)