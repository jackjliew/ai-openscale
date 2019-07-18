---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# 正解率モニターまたはモデル性能モニターの構成
{: #acc-monitor}

モデル性能モニター (以前は正解率モニターと呼ばれていました) を使用して、モデルの結果予測の精度を調べられます。
{: shortdesc}

## 構成手順
{: #acc-config}

**「正解率」**タブの**「正解率とは (What is Accuracy?)」**ページで、**「開始」**をクリックして、構成プロセスを開始します。

![「正解率モニターの説明」ページ](images/accuracy-what-is.png)

「正解率」構成タブの一連のページで以下の設定を構成します。

-  正解率のアラートしきい値を設定します。 許容可能な正解率のレベルを表す値を選択します。

    正解率とは、それぞれの特定のモデル・タイプに関連付けられている関連データ・サイエンスの指標から合成された値です。 スコアは正規化されているので、この指標を使用してさまざまなモデル・タイプの正解率を容易に比較できます。 標準的なモデルでは、正解率スコア 80 で十分です。
    {: note}

-  最大と最小のサンプル・サイズを設定します。 最小サイズを設定することにより、評価データ・セットで最小限の数のレコードを得られなければ、正解率の測定が行われなくなります。これにより、サンプル・サイズが小さすぎて結果にゆがみが生じることがなくなります。 最大サンプル・サイズを設定することにより、データ・セットの評価にかかる時間と労力の管理が楽になります。このサイズを超えた場合は最新のレコードだけが評価されます。


選択内容の要約が確認のために表示されます。 変更が必要な場合は、該当するセクションの**「編集」**リンクをクリックします。 そうでない場合は、**「保存」**をクリックして構成を完了します。

### 次のステップ
{: #acc-next}

**「モニターの構成」**ページで、別のモニタリング・カテゴリーを選択できます。
