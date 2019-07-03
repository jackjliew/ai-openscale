---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# PR 下的面积 ![beta 标记](images/beta.png)
{: #quality-area-pr}

查准率/查全率下的面积给出查准率和查全率曲线下的面积，这在类特别不平衡时有用。
{: shortdesc}

## PR 下的面积概览
{: #quality-area-pr-glance}

- **描述**：精度和查全率曲线下的面积
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵

## 解释显示内容
{: #quality-area-pr-display}

![显示 PR 下的面积，其中度量趋势向下](images/quality-area-under-pr.png)


## 测算
{: #quality-area-pr-math}

查准率/查全率下的面积给出 `Precision + Recall` 的总计。

查准率 (P) 定义为先计算真正 (Tp) 的数量加上假正 (Fp) 的数量之和，再用真正的数量除以和。

```
               number of true positives
Precision =   ______________________________________________________

              (number of true positives + number of false positives)
```

查全率 (R) 定义为先计算真正 (Tp) 的数量加上假负 (Fn) 的数量之和，再用真正的数量除以和。

```
            number of true positives
Recall =   ______________________________________________________

           (number of true positives + number of false negatives)
```
