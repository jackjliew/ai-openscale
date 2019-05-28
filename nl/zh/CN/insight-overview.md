---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 浏览仪表板
{: #io-ov}

您可以通过 {{site.data.keyword.aios_short}} 仪表板来跟踪正在监视的所有部署。该仪表板是 {{site.data.keyword.aios_short}} 的主要视图。该仪表板由五个选项卡组成：

  ![“洞察”选项卡](images/insight-tabs.png)

{: shortdesc}

## 洞察
{: #io-ins}

**洞察**选项卡 (![“洞察”仪表板](images/insight-dash-tab.png)) 提供部署监视的高级视图。

  ![“洞察”仪表板](images/insight-dashboard.png)

- ***受监视部署*** - 在此示例中，总共 10 个部署受到监视。10 个部署中的 8 个显示为下方的单独磁贴。

- ***准确性警报*** - 总共 3 个准确性警报通过紫色阴影在下方的磁贴中进行表示。在此示例中，`Driver Performance`、`Market Analytics` 和 `Pricing Risk` 部署显示“准确性”值分别为 `60%`、`65%` 和 `79%`。

- ***公平性警报*** - 总共有 6 个公平性警报，通过紫色阴影和 `BIAS` 小标记在下方的磁贴中进行表示。在此示例中，`Driver Performance`、`Market Analytics`、`Regulatory Compliance`、`Fraud Detection`、`Premium Optimization` 和 `Damage Cost Estimator` 部署显示“公平性”值分别为 `59%`、`68%`、`62%`、`64%`、`79%` 和 `63%`。

每个磁贴都提供该部署的监视活动摘要。请注意，`Call Center Routing` 部署磁贴不显示任何问题，表示模型相当稳定且准确。

### 后续步骤
{: #io-next}

选择任意单独的部署磁贴以查看有关该部署的更多详细信息。有关更多信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov)和[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

## 配置
{: #io-conf}

**配置**选项卡 (![“配置”选项卡](images/insight-config-tab.png)) 打开所选部署的配置摘要。

  ![配置摘要](images/insight-config-summary.png)

您可以从此处直接编辑部署监视器的配置设置。

## 事务
{: #io-tran}

使用**解释事务**选项卡 ( ![“解释事务”选项卡](images/insight-transact-tab.png) ) 可以搜索特定事务 ID 以解释特定部署事务。有关更多信息，请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

## AI 工具
{: #io-too}

使用 **AI 工具** 选项卡 (![“AI 工具”选项卡](images/aitools.png) ) 可以打开其他的 IBM AI 工具和选项。

- *[Watson Studio Lite 套餐 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*：Watson Studio 为您提供环境和工具以分析和可视化数据，对数据进行清理和塑形，摄入流式数据，或者创建、训练和部署机器学习模型。单击“注册免费 Watson Studio Lite 套餐”链接以获取 Watson Studio。

## “帮助”选项卡
{: #io-help}

“帮助”选项卡 (![“事务”选项卡](images/insight-help-tab.png)) 提供其他信息来帮助使用 {{site.data.keyword.aios_short}}。
