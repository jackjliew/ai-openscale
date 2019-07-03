---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: dashboard, navigating, navigation, insights

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

# 使用 {{site.data.keyword.aios_short}} 获取洞察
{: #io-ov}

您可以通过 {{site.data.keyword.aios_full}} 仪表板来跟踪正在监视的所有部署。该仪表板是 {{site.data.keyword.aios_short}} 的主要视图，并为您提供洞察模型性能的方式。
{: shortdesc}

## 洞察
{: #io-ins}

**洞察**选项卡 (![“洞察”仪表板](images/insight-dash-tab.png)) 提供部署监视的高级视图。

  ![“洞察”仪表板](images/insight-dashboard.png)

- ***受监视部署*** - 在此示例中，总共 10 个部署受到监视。在以下 10 个部署中，有 8 个显示为单独磁贴。

- ***准确性警报*** - 以下磁贴中总共表示 3 个准确性警报。在此示例中，`Driver Performance`、`Market Analytics` 和 `Pricing Risk` 部署显示“准确性”值分别为 `60%`、`65%` 和 `79%`。

- ***公平性警报*** - 总共有 6 个公平性警报，在以下磁贴中通过 `BIAS` 小标记进行表示。在此示例中，`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization` 和 `Damage Cost Estimator` 部署显示“公平性”值分别为 `59%`、`68%`、`62%`、`64%`、`79%` 和 `63%`。

每个磁贴都提供该部署的监视活动摘要。请注意，`Call Center Routing` 部署磁贴不显示任何问题，表示模型相当稳定且准确。

### 后续步骤
{: #io-next}

选择任意单独的部署磁贴以查看有关该部署的更多详细信息。有关更多信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov)和[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。



## 事务
{: #io-tran}

使用**解释事务**选项卡 ( ![“解释事务”选项卡](images/insight-transact-tab.png) ) 可以搜索特定事务 ID 以解释特定部署事务。有关更多信息，请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。


