---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 指標とトランザクションの分析 ![ベータ・タグ](images/beta.png)
{: #anlz_metrics}

{{site.data.keyword.aios_full}} を使用すると、さまざまな手段を使用して指標とトランザクションを分析できます。
{: shortdesc}

## 混同行列 ![ベータ・タグ](images/beta.png)
{: #it-conf-mtx}

品質指標の詳細情報として、モデルが誤って分析したレコードを表示することができます。 このような異常は、二項分類モデルの場合は誤検出か検出漏れである可能性があり、多項モデルの場合はクラスの割り当ての誤りの可能性があります。 モデルが正しく分析しなかったフィードバック・レコードのリストを表示することもできます。
{: shortdesc}

1. **「公平性」**などのいずれかの**「品質」**グラフから、グラフ内の時間/日をクリックします。
    
    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.004.png)

1. 混同行列に、誤検出と検出漏れが表示されます。 セルをクリックして、フィードバック・レコードのサブセットを表示します。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.005.png)

1. フィードバック・レコードを検討し、フィードバック・レコードに対する分析の説明を要求します。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.006.png)

1. トランザクションがインラインで表示されます。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.007.png)

