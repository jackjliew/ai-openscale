---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# 配置漂移检测监视器 ![beta 标记](images/beta.png)
{: #behavior-drift-config}

您必须配置 {{site.data.keyword.aios_full}} 漂移监视器，然后它才能开始分析模型。有两个选项：在线训练模型或使用笔记本。
{: shortdesc}

如果使用 {{site.data.keyword.pm_full}} 并且数据不超过 500 MB，那么可以通过使用 {{site.data.keyword.aios_short}} 来在线训练模型。否则，必须使用笔记本来训练模型。

## 在 {{site.data.keyword.aios_short}} 中配置漂移的步骤
{: #behavior-drift-config-steps-wos}

如果您使用 {{site.data.keyword.pm_full}}，那么可以选择使用 {{site.data.keyword.aios_short}} 用户界面来配置漂移检测。

1. 从**什么是漂移？**页面上的**漂移**选项卡中，单击**开始**以启动配置过程。

   ![“什么是漂移？”页面](images/wos-drift-config-1.png)

2. 单击**在 Watson OpenScale 中训练**磁贴。

   ![“什么是漂移？”页面](images/drift-config-2.png)

3. 设置警报阈值。

   ![“什么是漂移？”页面](images/drift-config-3.png)

3. 设置样本大小。

   ![“什么是漂移？”页面](images/drift-config-4.png)
   
3. 单击**保存**。


## 使用笔记本配置漂移的步骤
{: #behavior-drift-config-steps-ntbk}

如果使用除 {{site.data.keyword.pm_full}} 以外的其他机器学习提供程序（例如 Microsoft Azure、Amazon SageMaker 或定制机器学习引擎），那么必须使用笔记本来配置漂移检测。也可以通过使用此方法为 {{site.data.keyword.pm_full}} 配置漂移。

如果训练数据未存储在 Db2 或 {{site.data.keyword.cos_full}} 中，那么此选项有用。使用笔记本时，必须将训练数据读取到数据帧中。然后，可从 {{site.data.keyword.aios_short}} 下载的专用笔记本会创建可上载到 {{site.data.keyword.aios_short}} 的专用输出。

1. 创建笔记本以生成漂移检测模型。使用可从 {{site.data.keyword.aios_short}} UI 获取的[样本笔记本](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb)。
2. 使用压缩软件将漂移检测模型压缩成 .tar.gz 文件。

1. 从**什么是漂移？**页面上的**漂移**选项卡中，单击**开始**以启动配置过程。

   ![“什么是漂移？”页面](images/wos-drift-config-1.png)

2. 单击**在笔记本中训练**磁贴。

   ![带有联机选项和笔记本选项的漂移配置页面](images/drift-config-2.png)

3. 将压缩模型文件拖入到目标区域中，或者浏览以选择该文件并单击**下一步**。

   ![“什么是漂移？”页面](images/wos-drift-config-2b.png)
   
3. 上载漂移检测模型，然后单击**下一步**。

   ![“什么是漂移？”页面](images/drift-config-upload.png)
   
3. 设置警报阈值。

   ![“什么是漂移？”页面](images/drift-config-3.png)

3. 设置样本大小。

   ![“什么是漂移？”页面](images/drift-config-4.png)
   
3. 单击**保存**。

## 后续步骤
{: #behavior-drift-config-next-steps}

- 有关解释漂移的更多信息，请参阅[漂移量级](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
