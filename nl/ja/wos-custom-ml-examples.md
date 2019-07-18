---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# カスタム機械学習エンジンの例
{: #fmrk-workaround-cstmmlsengex}

以下の例を使用して、独自のカスタム機械学習エンジンをセットアップします。
{: shortdesc}

## Python と Flask
{: #fmrk-workaround-pandflask}

[Git で公開されたカスタム ML エンジンの例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)では、Python と Flask を使用して、scikit-learn モデルを提供します。

[README ファイル](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)では、テスト目的でアプリケーションをローカルにデプロイする方法、および IBM Cloud 上の cf アプリケーションについて説明します。 REST API エンドポイントの実装は、[app.py ファイル](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py)にあります。

## Node.js
{: #fmrk-workaround-nodejs}

[ここで、Node.js](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs) で作成されたカスタム機械学習エンジンの例を確認することもできます。

## エンドツーエンドのコード・パターン
{: #fmrk-workaround-e2ecode}

[コード・パターン](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale)で、カスタム・エンジンのデプロイメントおよび {{site.data.keyword.aios_short}} との統合のエンドツーエンドの例を示します。

