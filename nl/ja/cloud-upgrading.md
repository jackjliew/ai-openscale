---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: upgrading, configuration, configuring, deployment, subscription, service plans, plans

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

# ライト・プランから有料プランへの {{site.data.keyword.aios_short}} のアップグレード
{: #cf-upgrade}

{{site.data.keyword.Bluemix}} ダッシュボードを使用して、{{site.data.keyword.aios_full}} を無料のライト・プランから有料プランにアップグレードできます。アップグレードを実行する時期を把握する目安があります。それは、「`403 Errors.AIQFM0011: 'ライト・プランにおいて、バイアス修正の限度である 50,000 行を越えました`」などのエラー・メッセージが表示されるようになった時点です。
{: shortdesc}

1. {{site.data.keyword.aios_short}} ダッシュボードで各自のアバターをクリックします。
2. **「アップグレード・オプションを表示します」**をクリックします。
4. **「標準」**チェック・ボックスを設定し、**「アップグレード」**をクリックします。

アップグレードの完了後に、アップグレードが反映されるまで約 5 分かかります。この間にエラー・メッセージが表示されることがありますが、アップグレード後には、制限超過に関するエラー・メッセージは表示されなくなります。

## 次のステップ
{: #cf-upgrade-ns}

{{site.data.keyword.Bluemix}} サービスのアップグレードについて詳しくは、[サービス・プランの変更](/docs/resources?topic=resources-changing){: external}を参照してください。
