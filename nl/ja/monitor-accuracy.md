---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 正確度
{: #acc-monitor}

正確度により、モデルの予測の結果の精度を知ることができます。
{: shortdesc}

## 正確度について
{: #acc-understand}

以下のように、アルゴリズムのタイプに応じて正確度の意味は異なることがあります。

- *マルチクラス分類*: 正確度により、クラスが正しく予測された回数が、データ・ポイントの数で正規化されて測定されます。詳細については、Apache Spark 資料の [Multiclass classification ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification) を参照してください。

- *二項分類*: 二項分類アルゴリズムの場合、正確度は ROC 曲線の下の領域として測定されます。詳細については、Apache Spark 資料の [Binary classification ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification) を参照してください。

- *回帰*: 回帰アルゴリズムは、決定係数または R2 を使用して測定されます。詳細については、Apache Spark 資料の [Regression model evaluation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation) を参照してください。

### 動作内容
{: #acc-uhow}


下記のように {{site.data.keyword.aios_short}} UI により、または [Python クライアント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} を使用して、あるいは [Rest API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window} により、手動でラベル付けされたフィードバックを追加する必要があります。

正確度のモニターの制限について、[サポートされるモデル・タイプ](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mod)と[サポートされるフレームワーク](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)を確認してください。

## 正確度のモニターの構成
{: #acc-config}

1.  *「正確度は? (What is Accuracy?)」*ページから、**「次へ」**をクリックして構成プロセスを開始します。

    ![「正確度は? (What is Accuracy?)」ページ](images/accuracy-what-is.png)

1.  *「正確度しきい値の設定 (Set accuracy threshold)」*ページで、受け入れられる正確度レベルを表わす値を選択します。

    正確度の値は、個々の特定のモデル・タイプと関連付けられている関連データ・サイエンス・メトリックから同期されます。スコアとは、さまざまなモデル・タイプ間で正確度を簡単に比較できる、正規化された尺度のことです。典型的な状態では、正確度スコアは 80 で十分です。
    {: note}

    ![正確度の限度の設定](images/accuracy-set-limit.png)

    **「次へ」**をクリックして先に進みます。

1.  続いて、最小と最大のサンプル・サイズを設定します。最小サイズを設定すると、評価データ・セット内で最小限のレコード数が使用可能になるまでは正確度の測定が進まなくなり、サンプル・サイズが小さすぎて結果が偏るということはなくなります。最大サンプル・サイズを設定すると、このサイズを超えた場合に最新のレコードのみ評価されるので、データ・セットの評価に費やす時間や労力の管理性能を改善できます。

     ![サンプル・サイズの構成](images/accuracy-config-sample.png)

1.  **「次へ」**ボタンをクリックします。

    検討用に選択内容の要約が表示されます。変更する場合は、その選択項目に関する**「編集」**リンクをクリックします。

1.  **「保存」**をクリックし、構成を完了します。

この時点で、正確度を評価するために、フィードバック・データをモデルに直接提供するオプションが表示されます。

  ![フィードバック・データの送信](images/accuracy-send-feedback.png)

*「フィードバック・データの追加 (Add Feedback Data)」*ボタンを選択して、CSV 形式のデータ・ファイルをアップロードします。ご使用のデータと一致するように区切り文字を設定します。

フィードバック CSV ファイルには、すべてのフィーチャー値と、手動で割り当てられたターゲット/ラベル値があることが期待されます。例えば、薬モデルのトレーニング・データにはフィーチャー値 `"AGE"`、`"SEX"`、`"BP"`、`"CHOLESTEROL"`、`"NA"`、`"K"` とターゲット/ラベル値 `"DRUG"` が含まれています。フィードバック CSV ファイルに、例えば `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]` のような、これらのフィールドの値が組み込まれている必要があります。フィードバック CSV ファイルのヘッダーを提供すると、そのヘッダーを使用してフィールド名がマップされます。提供しない場合は、フィールドの順序はトレーニング・スキーマ内の順序と完全に同じで**なければなりません**。
{: important}

モデルが戻す予測タイプをメモしてください。フィードバック・データ内のターゲット/ラベル列が一致していなければなりません。
{: note}

  ![正確度の区切り文字](images/accuracy-delimit.png)

現在、ファイル・サイズは 8MB に制限されています。
{: note}

あるいは、提供されている `cURL` または `Python` コード・スニペットを使用してフィードバック・データをパブリッシュすることもできます。

コード・スニペット内のフィールドと値を、実際の値に置換する必要があります。提供されている値は例にすぎないからです。
{: important}

**「終了」**を選択して、このオプションのステップをスキップすることもできます。スキップしても、後で評価のために CSV ファイルをアップロードできます。

## 次のステップ
{: #acc-next}

*「モニターの構成」*ページから、別のモニター・カテゴリーを選択できます。
