---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R 平方
{: #quality_r_squared}

R 方是目标方差与预测误差方差之间的差值占目标方差的比率。它可以指示用于创建模型的数据与回归的拟合度。
{: shortdesc}

## R 方概览
{: #quality_r_squared-glance}

- **描述**：以下两个方差之间的差异比率：目标方差，预测误差和目标方差之间的方差
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：回归
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：无

## 解释显示内容
{: #quality_r_squared-display}

![显示 R 方图表。](images/xxxx.png)

## 测算
{: #quality_r_squared-math}

以下公式中定义了 R 方度量。

```
                  explained variation
R squared =ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service-  _____________________

                    total variation
```
