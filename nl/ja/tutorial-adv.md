---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Python SDK チュートリアル (上級)
{: #crt-ov}

このチュートリアルでは、以下のタスクの実行方法を取り上げます。

- 機械学習モデルの作成、トレーニング、デプロイのために Python ノートブックを実行します。
- データマートを作成し、パフォーマンス、正確度、公平性のモニターを構成し、モニター対象のデータを作成します。
- {{site.data.keyword.aios_short}} の「洞察」タブで結果を表示します。

## シナリオ
{: #crt-scenario}

従来型の金融業者は、さらに大規模でさらに多様な対象者層に向けて金融サービスのデジタル・ポートフォリオを拡張しなければならないというプレッシャーにさらされています。そのような拡張のためには、信用リスク・モデリングの新しい手法が必要です。データ・サイエンス・チームは、標準的なモデリング手法 (デシジョン・ツリーやロジスティック回帰など) に頼っていますが、こうした手法は、中規模のデータ・セットではうまく機能し、簡単に説明できる推奨事項の作成も可能です。クレジットに関する決定の透明性と説明可能性を確保しなければならないという法律要件にも対応できます。

より幅広くよりリスクの高い層に対してクレジット・アクセスを提供するには、申請者のクレジット・ヒストリーとして、従来型のクレジット (住宅ローンや自動車ローンなど) の枠を超えた詳細情報が必要になります。代替のクレジット・ソース (水道光熱費や携帯電話など) での支払い計画のヒストリーや、教育や役職などの情報です。こうした新しいデータ・ソースは魅力的ではありますが、リスクも伴います。申請者本人の年齢や性別や性格に基づくバイアスが入り込んで予想外の相関関係が発生する確率が高くなるからです。

こうした多様なデータ・セットに最適なデータ・サイエンスの手法 (こう配ブースティング・ツリーやニューラル・ネットワークなど) を使用すれば、非常に正確なリスク・モデルを生成できますが、コストがかかります。そのような「ブラック・ボックス」モデルからは、不透明な予測が生成されます。EU の一般データ保護規則 (GDPR) の第 22 条や米国の消費者金融保護局が管理する連邦政府の公正信用報告法 (FCRA) などの法令に基づく承認を得るには、そうした不透明な予測の透明性をいくらかでも高める必要があります。

このチュートリアルの信用リスク・モデルで使用するトレーニング・データ・セットには、ローンの申請者に関する 20 の属性が組み込まれています。そのうちの 2 つの属性 (年齢と性別) に関するバイアスをテストできます。このチュートリアルでは、性別と年齢に関するバイアスに焦点を合わせます。

{{site.data.keyword.aios_full}} for {{site.data.keyword.icpfull}} for Data を使用して、デプロイしたモデルを対象に、1 つのグループ (参照グループ) ともう 1 つのグループ (モニター対象グループ) で好ましい結果 (リスクなし) が得られる傾向をモニターします。このチュートリアルでは、性別のモニター対象グループとして`「女性」`、年齢のモニター対象グループとして`「18 歳から 25 歳」`を使用します。

## 前提条件
{: #crt-prereqs}

このチュートリアルでは、「Python 3.x with Spark」ランタイム環境で実行する Jupyter ノートブックを使用します。以下の {{site.data.keyword.icpfull}} for Data サービスのサービス資格情報が必要です。

- {{site.data.keyword.aios_short}}

- {{site.data.keyword.pm_full}}

  {{site.data.keyword.pm_short}} インスタンスをアカウントにまだ関連付けていない場合は、関連付けを行うことが必要です。[{{site.data.keyword.icpfull}} for Data インストールの一部としてプロビジョンされた機械学習サービス](ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#inst-wml)がある場合は、そのサービスが同じ組織とスペースに入っていることを確認してください。
  
- Db2 Warehouse
  
  Db2 Warehouse サービスをアカウントにまだ関連付けていない場合は、関連付けを行う必要があります。[{{site.data.keyword.icpfull}} for Data インストールの一部としてプロビジョンされた Db2 Warehouse サービス](ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#inst-db2)がある場合は、そのサービスが同じ組織とスペースに入っていることを確認してください。

前述の各 {{site.data.keyword.icpfull_notm}} for Data サービスのプランを選択する時には、幾つかのオプションがあります。ライト・プランもその 1 つです。ライト・プランは無料ですが、制約が多く、毎月の制限値に達する前にこのチュートリアルを数回実行する程度の処理しかできません。
{: note}

## 概要
{: #crt-intro}

ドイツの信用リスク・モデルのトレーニング、作成、デプロイのために Jupyter ノートブックを使用し、そのデプロイメントをモニターするために {{site.data.keyword.aios_short}} を構成し、7 日分の履歴のレコードと測定値を提供して {{site.data.keyword.aios_short}} の「洞察」ダッシュボードで表示します。

## 機械学習モデルを作成してデプロイする
{: #crt-make-model}

### `「Working with Watson Machine Learning」`ノートブックを好みのエディターに追加する
{: #crt-add-notebook}

1.  {{site.data.keyword.icpfull}} の[「Working with Watson Machine Learning」ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb){: new_window} をダウンロードします。
1.  {{site.data.keyword.DSX}} または Jupyter や Zeppelin の任意のノートブック・エディターでノートブックを開きます。{{site.data.keyword.DSX_full}} でノートブックを操作するための詳細については、[ノートブック](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/dsx/notebooks-parent.html)を参照してください。

### `「Working with Watson Machine Learning」`ノートブックを編集して実行する
{: #crt-edit-notebook}

{{site.data.keyword.icpfull}} の`「Working with Watson Machine Learning」`ノートブックには、実行する Python コードの各ステップに関する詳しい説明が含まれています。ノートブックの作業をする時に、時間を取って各コマンドの機能を確認してください。

1.  **「資格情報の構成」**セクションで以下の変更を加えます。
    1.  {{site.data.keyword.aios_short}} と {{site.data.keyword.pm_full}} の資格情報を実際の資格情報に置き換えます。
    1.  データベースの資格情報を Db2 Warehouse 用に作成した資格情報に置き換えます。
    1.  作成したスキーマの名前を追加します。

1.  資格情報を入力したら、ノートブックを実行する準備ができたことになります。ノートブックの各ステップを順序どおりに実行してください。各ステップで説明どおりに処理が行われていることを確認します。**「Additional data to help debugging」**セクションも含め、すべてのステップを完了してください。

これで、**「Spark German Risk Deployment- Final」**モデルを作成し、トレーニングして、{{site.data.keyword.aios_short}} サービス・インスタンスにデプロイしたことになります。その後、このモデルで性別 (この場合は「女性」) や年齢 (この場合は「18 歳から 25 歳」) に関するバイアスを確認するために {{site.data.keyword.aios_short}} を構成します。

## 結果の表示
{: #crt-view-results}

### デプロイメントの洞察を表示する
{: #crt-view-insights}

[{{site.data.keyword.aios_short}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} の**「洞察」**タブをクリックします。

  ![洞察](images/insight-dash-tab.png)

「洞察」ページに、デプロイしたモデルのメトリックの概要が表示されます。ノートブックの実行時に設定したしきい値を下回った公平性や正確度のメトリックに関するアラートも表示できます。このチュートリアルで使用するデータや設定では、正確度や公平性に関して以下のようなメトリックが作成されます。

  ![洞察の概要](images/insight-overview-adv-tutorial-2.png)

### デプロイメントのモニター・データを表示する
{: #crt-view-mon-data}

**「洞察」**ページでタイルをクリックしてデプロイメントを選択します。そのデプロイメントのモニター・データが表示されます。チャートの上でマーカーをスライドさせれば、1 時間枠のデータを選択できます。その後、**「詳細の表示」**リンクを選択してください。

  ![モニター・データ](images/insight-monitor-data2.png)

チャートでモニター・データを確認すると、「性別」の特色については、`女性`のグループの方が`男性`のグループよりも、「リスクなし」という好ましい結果を得た比率が若干低くなっています (女性が 74% に対して男性が 78%)。

  ![洞察の概要](images/insight-review-charts2.png)

### モデル・トランザクションの説明可能性を表示する
{: #crt-view-explain}

デプロイメントごとに、特定のトランザクションの説明可能性データを確認できます。

表示対象のトランザクションが分かっている場合は、トランザクション ID を使用するのが手っ取り早い方法です。デプロイメントのタイルをクリックし、ナビゲーターから**「トランザクションの説明」** ![「トランザクションの説明」タブ](images/insight-transact-tab.png) アイコンをクリックし、トランザクション ID を入力し、**Enter** を押します。
{: tip}

最新のバイアス・データを確認するには、チャートから**「トランザクションの表示」**ボタンをクリックします。

  ![トランザクションの表示](images/view_transactions.png)

  デプロイメントでバイアスのかかった部分が存在するトランザクションのリストが表示されます。トランザクションを 1 つ選択して、**「説明」**リンクをクリックしてください。

  ![トランザクション・リスト](images/transaction_list_cr.png)

モデルでその結論が得られた理由の説明が表示されます。その説明には、モデルの信頼度、その信頼度レベルになった要因、モデルに提供された属性などが含まれます。

  ![トランザクションの表示](images/view_transaction_cr.png)

## 次のステップ
{: #crt-next-steps}

- [データの表示と解釈](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)と[説明可能性のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)の学習に進んでください。
