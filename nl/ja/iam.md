---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


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

アカウント内のユーザーによる {{site.data.keyword.aios_full}} サービス・インスタンスへのアクセスは、 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) によって制御されます。アカウント内の {{site.data.keyword.aios_short}} サービスにアクセスするすべてのユーザーに、IAM 役割を定義したアクセス・ポリシーを割り当てる必要があります。選択したサービスまたはインスタンスのコンテキスト内でユーザーが実行できるアクションは、ポリシーによって決まります。許可されるアクションは、{{site.data.keyword.Bluemix_notm}} サービスで実行することを許可される操作として、このサービスによってカスタマイズされ、定義されます。その後、アクションが IAM ユーザー役割にマップされます。

ポリシーを使用して、さまざまなレベルのアクセス権限を付与することができます。次のようなオプションがあります。 

* アカウント内のすべてのサービスに対するアクセス権限
* アカウント内の個々のサービス・インスタンスに対するアクセス権限
* インスタンス内の個々のリソースに対するアクセス権限

アクセス・ポリシーの範囲を定義したら、ユーザーのアクセス・レベルを決定する役割を割り当てます。以下の各表に、{{site.data.keyword.aios_short}} サービスで許可されるアクションを役割別に記載します。

次の表は、プラットフォームの管理役割にマップされているアクションの詳細を示しています。
プラットフォームの管理役割を持つユーザーは、プラットフォーム・レベルでサービス・リソースに対してタスクを実行できます。例えば、サービスに対するアクセス権限をユーザーに割り当てたり、インスタンスを作成/削除したり、アプリケーションにインスタンスをバインドしたりできます。


| プラットフォームの管理役割 | アクションの説明 | アクションの例                                                 |
|--------------------------|------------------------|-----------------------------------------------------------------|
| ビューアー               | 説明            | <ul><li>例 1</li><li>例 2</li></ul>                   |
| エディター               | 説明            |<ul><li>例 1</li><li>例 2</li></ul>                    |
| オペレーター             | 説明            | <ul><li>例 1</li><li>例 2</li><li>例 3</li></ul> |
| 管理者                   | 説明            |<ul><li>例 1</li><li>例 2</li><li>例 3</li></ul>  |
{: caption="表 1. IAM ユーザー役割とアクション" caption-side="top"}


次の表は、サービスのアクセス役割にマップされているアクションの詳細を示しています。サービスのアクセス役割を持つユーザーは、{{site.data.keyword.aios_short}} にアクセスすること、また、{{site.data.keyword.aios_short}} API を呼び出すことができます。

| サービスのアクセス役割 | アクションの説明 | アクションの例                                                 |
|---------------------|------------------------|-----------------------------------------------------------------|
| リーダー            | 説明            | <ul><li>例 1</li><li>例 2</li></ul>                   |
| ライター            | 説明            |<ul><li>例 1</li><li>例 2</li></ul>                    |
| 管理者              | 説明            | <ul><li>例 1</li><li>例 2</li><li>例 3</li></ul> |
{: caption="表 2. IAM サービスのアクセス役割とアクション" caption-side="top"}


UI でユーザーの役割を割り当てる方法については、[リソースへのアクセスの管理](/docs/iam?topic=iam-iammanidaccser#iammanidaccser)を参照してください。

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
