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

# モデル性能 (正確度) モニタリングの構成
{: #acc-monitor}

モデル性能モニタリング (以前は正確度モニタリングと呼ばれていました) を使用して、モデルの結果予測の精度を調べることができます。
{: shortdesc}

## 構成手順
{: #acc-config}

**「品質」**タブの**「モデル性能モニタリングとは (What is the Quality monitor?)」**ページで、**「開始」**をクリックして公正プロセスを開始します。

![「モデル性能モニタリングとは (What is the Quality monitor?)」ページが表示されます。このページでは、モデルがどの程度正確な結果を予測するかがモデル性能モニタリングによって評価されることを説明しています](images/wos-quality-what-is.png)

「正解率」構成タブの一連のページで以下の設定を構成します。

-  正解率のアラートしきい値を設定します。 許容可能な正解率のレベルを表す値を選択します。たとえば、対話式チュートリアルで **German Credit Risk モデル**を使用する場合は、アラートを **90%** に設定します。
    正解率とは、それぞれの特定のモデル・タイプに関連付けられている関連データ・サイエンスの指標から合成された値です。 スコアは正規化されているので、この指標を使用してさまざまなモデル・タイプの正解率を容易に比較できます。 標準的なモデルでは、正解率スコア 80 で十分です。チュートリアルでは、さらにデータを生成するために 90 が推奨されます。{: note}

-  最大と最小のサンプル・サイズを設定します。 最小サイズを設定することにより、評価データ・セットで最小限の数のレコードを得られなければ、正解率の測定が行われなくなります。これにより、サンプル・サイズが小さすぎて結果にゆがみが生じることがなくなります。 最大サンプル・サイズを設定することにより、データ・セットの評価にかかる時間と労力の管理が楽になります。このサイズを超えた場合は最新のレコードだけが評価されます。たとえば、対話式チュートリアルで **German Credit Risk モデル**を使用する場合は、最小サンプル・サイズを **100** に、最大サンプル・サイズを **10000** に設定します。


選択内容の要約が確認のために表示されます。 変更が必要な場合は、該当するセクションの**「編集」**リンクをクリックします。 そうでない場合は、**「保存」**をクリックして構成を完了します。

### 次のステップ
{: #acc-next}

モニタリングの構成を続けるには、**「公平性」**タブをクリックし、**「開始」**をクリックします。詳しくは、[公平性モニターの構成](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。
