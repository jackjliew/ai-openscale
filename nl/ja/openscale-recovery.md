---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# 高可用性と災害復旧
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} は、ダラス、ワシントン DC など、複数の {{site.data.keyword.cloud_notm}} ロケーションで高可用性を備えています。 ただし、1 つの場所全体に影響を及ぼす可能性のある災害からの復旧には計画と準備が必要になります。
{: shortdesc}

サービスに関するご自身の構成、カスタマイズ内容、使用法を把握しておくのはお客様の責任です。 また、新しい場所でサービスのインスタンスを再作成したり、いずれかの場所にデータを復元したりする準備をしておくのもお客様の責任です。 詳しくは、[ダウン時間をゼロにする方法 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} を参照してください。

##高可用性 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} は、3 つのアベイラビリティー・ゾーンで複数ゾーン・ルーティング (MZR) を行う **us-south** データ・センターにデプロイされ、利用できます。 どの時点においても、1 つのゾーンが利用できなくなっても、他のアベイラビリティー・ゾーンを使用して引き続きシステムを利用できます。 ユーザーが介入しなくても、トラフィックはグローバル・ロード・バランサーと DNS サーバーによって使用可能なゾーンにルーティングされます。

PostgreSQL データベースに格納されているデータも高可用性があり、複数のアベイラビリティー・ゾーンに配置されます。 ただし、災害復旧計画の一環としてサービスを再作成できるようにデータをバックアップしておくのは、お客様の責任です。

{{site.data.keyword.aios_short}} トラフィックは、1 つの地域の複数のゾーンでロード・バランシングが行われます。 各ゾーンは、同じ地域に属する 1 つのデータ・センターです。 

PostgreSQL データベースや分散 <code>etc</code> ディレクトリー (etcd) データベースなどのデータベースを定期的にバックアップするように構成して高可用性を確保してください。そのような備えがあれば、災害時に {{site.data.keyword.aios_short}} 運用チームは、目標復旧時点 (RPO) の範囲内でサービスを復旧できます。
 
{{site.data.keyword.cloud_notm}} は、地域内データの冗長性を備えているので、高可用性の保護が可能になります。 IBM は追加費用なしで、訓練データやカスタム・モデル・データを格納するクライアント・データベース向けの自動データ・レプリケーション機能を提供しています。 レプリケーションは、地域内アベイラビリティー・ゾーンにある {{site.data.keyword.cloud_notm}} データ・センターの間で行われます。
 
## バックアップとリストア
{: #openscale-restore}

訓練データ、カスタム・モデル・データ、クライアント生成カスタム・モデルなど、自分のデータをバックアップおよびリストアするのはお客様の責任です。 クライアントのバックアップとリストアの手順については、{{site.data.keyword.cloud_notm}} の資料を参照してください。
 
##災害復旧
{: #openscale-disaster-recovery}

地域内の事業継続性は、地域内アベイラビリティー・ゾーンにある {{site.data.keyword.cloud_notm}} データ・センターの間で自動レプリケーションを利用することによって確保されます。 複数地域の災害復旧はお客様の責任です。 この責任には、自分のセキュリティー・ポリシー、訓練データ、カスタム・モデル・データ、クライアント生成カスタム・モデルのバックアップ、リストア、同期を行うことも含まれます。 加えて、地域間におけるルーティングやロード・バランシングを行うのもお客様の責任です。 クライアントのバックアップとリストアの手順については、{{site.data.keyword.cloud_notm}} の資料を参照してください。
