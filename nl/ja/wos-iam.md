---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Identity and Access Management の役割とアクション

アカウント内のユーザーによる {{site.data.keyword.aios_full}} サービス・インスタンスへのアクセスは、 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) によって制御されます。 アカウント内の {{site.data.keyword.aios_short}} サービスにアクセスするすべてのユーザーに、IAM 役割を定義したアクセス・ポリシーを割り当てる必要があります。 選択したサービスまたはインスタンスのコンテキスト内でユーザーが実行できるアクションは、ポリシーによって決まります。 許可されるアクションは、{{site.data.keyword.Bluemix_notm}} サービスで実行することを許可される操作として、このサービスによってカスタマイズされ、定義されます。 その後、アクションが IAM ユーザー役割にマップされます。

ポリシーを使用して、さまざまなレベルのアクセス権限を付与することができます。 次のようなオプションがあります。 

* アカウント内のすべてのサービスに対するアクセス権限
* アカウント内の個々のサービス・インスタンスに対するアクセス権限
* インスタンス内の個々のリソースに対するアクセス権限

アクセス・ポリシーの範囲を定義したら、ユーザーのアクセス・レベルを決定する役割を割り当てます。 以下の各表に、{{site.data.keyword.aios_short}} サービスで許可されるアクションを役割別に記載します。

プラットフォーム管理の役割では、アカウント内またはサービスでプラットフォーム・アクションを実行するためのさまざまなレベルの許可をユーザーに割り当てることができます。 例えば、カタログ・リソース用に割り当てられたプラットフォーム管理の役割により、ユーザーは、サービス・インスタンスの作成、削除、編集、および表示などのアクションを実行できるようになります。 また、アカウント管理サービス用に割り当てられたプラットフォーム管理の役割により、ユーザーは、ユーザーの招待と削除、リソース・グループの操作、請求情報の表示などのアクションを実行できるようになります。 アカウント管理サービスについて詳しくは、[アカウント管理サービスへのアクセス権限の割り当て](/docs/iam?topic=iam-account-services#account-services){: external}を参照してください。

ポリシーの作成時に、該当するすべての役割を選択します。 各役割は個別にアクションの実行を許可します。下位の役割のアクションを継承することはありません。
{: tip}

以下の表に、カタログのリソースおよびリソース・グループに関してユーザーが実行できるプラットフォーム管理アクションの例をいくつか示します。 使用するサービスのコンテキストで役割がどのようにユーザーに適用されるのかを調べるには、各カタログ・オファリングの資料を参照してください。


|  | 1 つまたはすべての IAM 対応サービス | リソース・グループ内の選択されたサービス | 選択されたリソース・グループ |
|:--------------|:------------|:-------------|:-------------|
| ビューアー役割 | インスタンス、別名、バインディング、および資格情報の表示 | リソース・グループ内の指定されたインスタンスのみの表示 | リソース・グループの表示 |
| オペレーター役割 |  インスタンスの表示と、別名、バインディング、および資格情報の管理 |  適用外 | 適用外 |
| エディター役割 |  インスタンスの作成、削除、編集、および表示。 別名、バインディング、および資格情報の管理 | リソース・グループ内の指定されたインスタンスのみの作成、削除、編集、一時停止、再開、表示、およびバインド | リソース・グループ名の表示および編集 |
| 管理者役割 |  サービスに対するすべての管理アクション | リソース・グループ内の指定されたインスタンスに対するすべての管理アクション | リソース・グループのアクセス権限の表示、編集、および管理 |
| クラスター管理者の役割 ({{site.data.keyword.wos4d_full}} のみ) |  IBM Cloud Private プラットフォームに対する完全なアクセス権限を持つ | リソース・グループ内の指定されたインスタンスに対する完全なアクセス権限を持つ | クラスター管理者のみが実行できるアクション: LDAP ディレクトリーへの接続、ユーザーの追加と IAM 役割の割り当て、すべての名前空間でのワークロード、インフラストラクチャー、アプリケーションの管理、名前空間の作成、割り当て量の割り当て、ポッド・セキュリティー・ポリシーの追加、内部 Helm リポジトリーの追加、内部 Helm リポジトリーの削除、内部 Helm リポジトリーへの Helm チャートの追加、内部 Helm リポジトリーからの Helm チャートの削除、内部 Helm リポジトリーと外部 Helm リポジトリーの同期 |
{: row-headers}
{: class="comparison-table"}
{: caption="表 1. アカウント内のサービスに対するプラットフォーム管理の役割とアクションの例" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


サービスのアクセス役割 ({{site.data.keyword.aios_short}} へのアクセスと REST API の呼び出しをユーザーに許可する役割) については 、{{site.data.keyword.aios_short}} は、上記の表にリストされているプラットフォーム管理の役割に従います。 UI でユーザーの役割を割り当てる方法については、[リソースへのアクセスの管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}を参照してください。

 
