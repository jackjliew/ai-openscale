---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# 对数损失 ![beta 标记](images/beta.png)
{: #quality_log_loss}

对数损失给出对数目标类概率（置信度）的平均值。它也称为预期对数似然，并且是模型性能的一项有效度量。
{: shortdesc}

## 对数损失概览
{: #quality_log_loss-glance}

- **描述**：对数目标类概率（置信度）的平均值。也称为预期对数似然。
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在恶化。反馈数据正在变得明显不同于训练数据。
   - **下降趋势**：下降趋势表明度量正在改善。 这意味着，模型再训练是有效的。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类和多类分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：无

## 解释显示内容
{: #quality_log_loss-display}

![显示对数损失](images/quality-log-loss.png)

## 测算
{: #quality_log_loss-math}

对于二元模型，使用以下公式计算对数损失：

```
-(y log(p) + (1-y)log(1-p))
```

其中 p = true 标签，y = 预测概率

对于多类模型，使用以下公式计算对数损失：

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

其中 M > 2，p = true 标签，y = 预测概率
