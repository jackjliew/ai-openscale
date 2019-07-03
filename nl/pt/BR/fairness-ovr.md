---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Visão geral das métricas de justiça
{: #anlz_metrics_fairness}

Use o monitoramento de justiça do {{site.data.keyword.aios_full}} para determinar se os resultados produzidos por seu modelo são justos ou não para o grupo monitorado. Quando o monitoramento de justiça é ativado, ele gera um conjunto de métricas a cada hora, por padrão. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.
{: shortdesc}

O {{site.data.keyword.aios_short}} identifica automaticamente se algum atributo protegido conhecido está presente em um modelo. Quando o {{site.data.keyword.aios_short}} detecta esses atributos, ele recomenda automaticamente a configuração de monitores de propensão para cada atributo presente, a fim de assegurar que a propensão com relação a esses atributos potencialmente sigilosos seja rastreada na produção. 

Atualmente, o {{site.data.keyword.aios_short}} detecta e recomenda monitores para os atributos protegidos a seguir: 

- sexo
- etnia
- estado civil
- idade
- CEP

Além de detectar atributos protegidos, o {{site.data.keyword.aios_short}} recomenda quais valores dentro de cada atributo devem ser configurados como os valores monitorados e os valores de referência. Portanto, por exemplo, o {{site.data.keyword.aios_short}} recomenda que, dentro do atributo "Sex", o monitor de propensão seja configurado de forma que "Woman" e "Non-Binary" sejam os valores monitorados e "Male" seja o valor de referência. Se desejar mudar qualquer uma das recomendações, será possível editá-las por meio do painel de configuração de propensão. 

Os monitores de propensão recomendados ajudam a acelerar a configuração e a assegurar que você está verificando seus modelos de IA para serem justos com relação a atributos sigilosos. À medida que os reguladores começam a ficar mais atentos à propensão algorítmica, torna-se cada vez mais crítico que as organizações tenham um claro entendimento de como seus modelos estão funcionando e se estão produzindo resultados injustos para determinados grupos. 

As métricas de justiça são calculadas com base nas informações a seguir:

- pontuação de dados de carga útil.

Para o propósito de monitoramento adequado, cada solicitação de pontuação também deve ser
registrada no {{site.data.keyword.aios_short}}. A criação de log de dados de carga útil é automatizada para mecanismos do {{site.data.keyword.pm_full}}.

Para outros mecanismos de aprendizado de máquina, os dados de carga útil podem ser fornecidos, usando o cliente Python ou a API de REST.

Para mecanismos de aprendizado de máquina diferentes do {{site.data.keyword.pm_full}}, o monitoramento de justiça cria solicitações de pontuação adicionais na implementação monitorada.
{: note}

É possível revisar todos os valores de métricas ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/fairness_metrics_001.png)

É possível revisar detalhes relacionados, tais como resultados favoráveis e desfavoráveis:

![detalhes de justiça](images/fairness_metrics_002.png)

É possível visualizar transações detalhadas:

![um gráfico que mostra uma lista de transações](images/fairness_metrics_003.png)

É possível visualizar o terminal de pontuação sem propensão recomendado:

![detalhes do terminal de pontuação sem propensão](images/fairness_metrics_004.png)

### Métricas de justiça suportadas
{: #anlz_metrics_supfairmets}

As métricas de justiça a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

- [Justiça para um grupo](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

Os atributos protegidos a seguir são suportados pelo {{site.data.keyword.aios_short}}: 

- [sexo](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [etnia](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [estado civil](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [idade](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [CEP](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### Detalhes de justiça suportados
{: #anlz_metrics_supfairdets}

Os detalhes a seguir para as métricas de justiça são suportados pelo {{site.data.keyword.aios_short}}:

- As porcentagens favoráveis para cada um dos grupos
- Médias de justiça para todos os grupos de justiça

```
                          (% de resultados favoráveis no grupo monitorado
Razão de impacto desproporcional =  ____________________________________________
                          (% de resultados favoráveis no grupo de referência)
```

- Distribuição dos dados para cada um dos grupos monitorados
- Distribuição de dados de carga útil
