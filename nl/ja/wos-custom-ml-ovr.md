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

# カスタム機械学習エンジン
{: #fmrk-workaround-customengine}

カスタム機械学習エンジンは、機械学習モデルと Web アプリケーションのインフラストラクチャーとホスティング機能を提供します。 {{site.data.keyword.aios_short}} によってサポートされるカスタム機械学習エンジンは、以下の要件に準拠している必要があります。

- 次の 2 つのタイプの REST API エンドポイントを公開します。

   * ディスカバリー・エンドポイント (デプロイメントと詳細の GET リスト)
   * 評価エンドポイント (オンラインでリアルタイムの評価)

- すべてのエンドポイントは、サポートされる swagger の仕様と互換性がある必要があります。

- 入力ペイロードと、デプロイメントへの出力およびデプロイメントからの出力は、仕様で説明された JSON ファイル形式に準拠している必要があります。

この段階では、`BasicAuth` フォーマットまたは `none` フォーマットのみがサポートされます。
{: Note}

以下の例は、REST API エンドポイント仕様を示しています。

![swagger ドキュメントから表示される REST API エンドポイント仕様](images/wosdeployments.png)


以下の例は、入力ペイロードのフォーマットを示しています。

![入力ペイロードの例が示されます](images/wosinputdata.png)


## カスタム機械学習エンジンが自分にとって最善の選択肢になる状況
{: #fmrk-workaround-enging-choice}

カスタム機械学習エンジンは、以下の状況が当てはまるときに最善の選択肢になります。

- 出来合いの製品を使用せずに、機械学習モデルを提供する場合。 また、これを行うための独自のシステムを開発したばかりである場合。 {{site.data.keyword.aios_short}} は、これを直接的にサポートせず、将来サポートする予定もありません。
- ご使用のサード・パーティーのサプライヤーからのサービス提供エンジンが、まだ {{site.data.keyword.aios_short}} でサポートされていない場合。 この場合は、元のデプロイメントまたはネイティブ・デプロイメントに対するラッパーとして、カスタム機械学習エンジンを開発することを検討してください。

## 次のステップ
{: #fmrk-workaround-nxt-steps-over}

[カスタム機械学習の例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)のいずれかを使用して、独自のソリューションを実装します。
