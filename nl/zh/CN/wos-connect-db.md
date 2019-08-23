---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# 指定数据库
{: #connect-db}

指定供 {{site.data.keyword.aios_short}} 实例使用的数据库。
{: shortdesc}

## 连接到数据库
{: #cdb-connect}

{{site.data.keyword.aios_short}} 使用数据库来存储载荷、反馈和度量数据。除选择数据库以外，您还可以为数据库选择模式 - 模式是数据库中表的命名集合。

1.  选择数据库。您有两个选项：免费数据库，或者现有数据库或新数据库。

    ![显示“选择数据库”屏幕，其中包含两个选项，指示使用免费 Lite 套餐或使用现有数据库](images/gs-config-database.png)

    如果您具有付费的 {{site.data.keyword.cloud_notm}} 帐户，那么可以供应 `Databases for PostgreSQL` 或 `Db2 Warehouse` 服务来充分利用与 Watson Studio 和持续学习服务的集成。如果选择不供应付费服务，那么可以将免费内部 PostgreSQL 存储与 {{site.data.keyword.aios_short}} 配合使用，但是将无法为模型配置持续学习。
    {: note}

### 免费 Lite 套餐数据库
{: #cdb-lite}

**注意**：免费数据库具有一些重要限制：

- 免费数据库受托管，您无法直接访问。
- {{site.data.keyword.aios_full}} 将对您的数据库具有完全访问权，因此对您的数据具有完全访问权。
- 免费数据库不符合 GDPR。如果模型处理个人可识别信息 (PII)，那么不能使用免费数据库。您必须购买新数据库，或者使用符合 GDPR 规则的现有数据库。请参阅[信息安全性](/docs/services/ai-openscale?topic=ai-openscale-is-ov)以了解更多信息。

要继续使用免费数据库，请单击**使用免费 Lite 套餐数据库**磁贴，然后单击**保存**。

  ![显示“已保存数据库”弹出消息，并已选定“选择提供程序”按钮](images/gs-config-database2.png)
  
可以从免费数据库升级到其他数据库，但无法将 Compose for Postgres、Database for Postgres 或 Db2 实例重新配置为免费数据库。升级之后，便无法再次使用免费数据库。并非所有当前数据（例如配置、评分结果和说明）都能重复使用。通过选择另一个模式或数据库，{{site.data.keyword.aios_short}} 环境将完全重置。



### 现有或新数据库
{: #cdb-exn}

1.  选择**使用现有数据库或购买新数据库**选项后，{{site.data.keyword.aios_short}} 会检查 {{site.data.keyword.Bluemix_notm}} 帐户以查找任何现有数据库。

1.  选择现有数据库类型（Compose for Postgres、Database for Postgres 或 Db2），再从**数据库**下拉菜单中选择数据库，然后选择**模式**：

    {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 数据库来存储模型相关数据（反馈数据或评分有效内容）和计算的度量。当前不支持 Lite Db2 套餐。有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![显示“选择数据库”屏幕，其中包含用于输入数据库类型、数据库名称和模式的字段。](images/gs-config-database3.png)

1.  您还可以单击**选择其他位置**以在 {{site.data.keyword.Bluemix_notm}} 帐户之外指定数据库位置。

    {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 数据库来存储模型相关数据（反馈数据或评分有效内容）和计算的度量。当前不支持 Lite Db2 套餐。
    {: note}

    - 选择**数据库类型**（`Compose for PostgreSQL`、`Database for PostgreSQL` 或 `Db2`），然后提供连接信息：

        - 对于 `Compose for PostgreSQL` 数据库，请完成以下操作：

            - 主机名或 IP 地址
            - 端口
            - 数据库（名称）
            - 用户名
            - 密码

        - 对于 `Database for PostgreSQL` 数据库，请完成以下操作：

            - 主机名或 IP 地址
            - SSL 端口
            - Base-64 编码证书
            - 数据库（名称）
            - 用户名
            - 密码

        - 对于 `Db2` 数据库，请完成以下操作：

            - 主机名或 IP 地址
            - SSL 端口
            - 数据库（名称）
            - 用户名
            - 密码

    - 成功连接后，可以选择模式并保存工作。

      如果提供具有有限访问权的 Db2 实例，那么需要显式提供模式名称，这不允许自动生成模式名称。这适用于 Entry Db2 Warehouse 套餐。
      {: important}

## 后续步骤
{: #cdb-next}

{{site.data.keyword.aios_short}} 现在可供您用于[发送评分有效内容](/docs/services/ai-openscale?topic=ai-openscale-cdb-score)和[为部署配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
