---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Explicações contrastantes usam positivos pertinentes e negativos pertinentes
{: #ie-pp-pn}

Para explicações contrastivas, o {{site.data.keyword.aios_short}} exibe valores positivos pertinentes e valores negativos pertinentes. 
{: shortdesc}

- Os positivos pertinentes são descobertas que são críticas para determinar o que é algo.
- Negativos pertinentes são não descobertas que são importantes por sua ausência.

O {{site.data.keyword.aios_short}} sempre exibe um positivo pertinente, no entanto, às vezes, não há nenhum negativo pertinente a ser exibido. Nesse caso, os valores para esse recurso já estão na mediana ou a predição não foi mudada como resultado da movimentação de valores para longe da mediana.

Para entender melhor, considere que, quando o {{site.data.keyword.aios_short}} calcula o valor negativo pertinente, ele muda os valores de todos os recursos para longe de seu valor mediano. Para os negativos pertinentes, isso significa os valores de recurso que estão mais distantes da mediana. Se os valores de um ponto de dados já estiverem na mediana ou, mesmo depois de mudar o valor para longe da mediana, a predição não mudar, então não haverá nenhum negativo pertinente a ser exibido. No caso de positivos pertinentes, o {{site.data.keyword.aios_short}} localiza a mudança máxima nos valores de recurso em relação à mediana, de modo que a predição não muda. Na prática, isso significa que há quase sempre um positivo pertinente para explicar uma transação.

