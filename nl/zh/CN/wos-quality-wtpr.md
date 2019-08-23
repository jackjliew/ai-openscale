---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 加权真正率 (wTPR)
{: #quality-wtpr}

加权真正率给出权重等于类概率的 TPR 类的加权平均值。
{: shortdesc)

## 加权真正率 (wTPR) 概览
{: #quality-wtpr-glance}

- **描述**：权重等于类概率的类 TPR 的加权平均值
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：多类分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality-wtpr-display}

![显示加权真正率](images/quality-tpr.png)

## 测算
{: #quality-wtpr-math}

通过以下公式计算真正率：

```
                  number of true positives
TPR =  _________________________________________________________

        (number of true positives + number of false negatives)
```
