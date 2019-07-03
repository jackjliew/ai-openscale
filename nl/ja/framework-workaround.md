---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# サード・パーティーの ML エンジンと {{site.data.keyword.aios_short}} の統合
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} は、Microsoft Azure ML Studio や Amazon SageMaker などの外部の機械学習サービス・エンジンと統合します。
{: shortdesc}

以下の方法で、{{site.data.keyword.aios_short}} をサード・パーティー・エンジンと統合することができます。

- エンジンのバインディングのレベル: デプロイメントをリストして、デプロイメントの詳細を取得できます。
  
- デプロイメントのサブスクリプションのレベル: {{site.data.keyword.aios_short}} は、サブスクライブしたデプロイメントを {{site.data.keyword.pm_full}} フォーマットなどの必要なフォーマットで評価して、対応する同じ形式で出力を受信できる必要があります。{{site.data.keyword.aios_short}} は、入力フォーマットと出力フォーマットの両方を処理するように構成する必要があります。
   

- ペイロード・ロギング: ユーザーのアプリケーションでトリガーされたデプロイ済みモデルへの各入出力を、ペイロード・ストアに保管する必要があります。ペイロード・レコードのフォーマットは、上記のデプロイメント・サブスクリプション・レベルに関するセクションで説明したものと同じ仕様に従います。
   
   {{site.data.keyword.aios_short}} では、これらのレコードを使用してバイアスや説明などを計算します。 {{site.data.keyword.aios_short}} は、{{site.data.keyword.aios_short}} システムの外部にあるユーザー・サイトで実行されたトランザクションを自動的に保管することはできません。 これは、{{site.data.keyword.aios_short}} が専有情報を保護する方法の 1 つです。 {{site.data.keyword.aios_short}} Rest API または Python SDK を使用して、セキュア・データを処理します。
   
## このソリューションを実装する手順
{: #fmrk-workaround-steps}

1. [カスタム機械学習エンジンについて学習します](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine)。
2. [ペイロードのロギングをセットアップします](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload)。
3. [ペイロードのロギングを自動化します](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)。
4. [カスタム機械学習エンジンの例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)のいずれかを使用して、カスタム機械学習エンジンをセットアップします。

