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

# Analisando métricas e transações ![tag beta](images/beta.png)
{: #anlz_metrics}

É possível usar o {{site.data.keyword.aios_full}} para analisar métricas e transações por meio de uma variedade de formas.
{: shortdesc}

## Métricas de justiça
{: #anlz_metrics_fairness}

Use o monitoramento de justiça para determinar se os resultados que são produzidos por seu modelo são justos ou não para o grupo monitorado. Quando o monitoramento de justiça é ativado, ele gera um conjunto de métricas a cada hora, por padrão. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.

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

#### Justiça para um grupo
{: #anlz_metrics_supfairmets_group}

- **Descrição**: a propensão dos modelos para entregar resultados favoráveis para um grupo e não a outro.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**: nó de terminal de pontuação sem propensão que você pode usar em seu aplicativo de negócios para receber respostas sem propensão de seu modelo implementado.
- **Tipo de problema**: todos
- **Tipo de dados**: estruturado
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: sim

### Detalhes de justiça suportados
{: #anlz_metrics_supfairdets}

Os detalhes a seguir para as métricas de justiça são suportados pelo {{site.data.keyword.aios_short}}:

- As porcentagens favoráveis para cada um dos grupos
- Médias de justiça para todos os grupos de justiça

  Razão de impacto díspar = (% do resultado favorável no grupo monitorado) / (% do resultado favorável no grupo de referência)

- Distribuição dos dados para cada um dos grupos monitorados
- Distribuição de dados de carga útil


<!---
BTW, I propose to use screenshots with data from FastPath.
Source monitored group or referenced group
Source of bias is also in fairness metrics
--->


## Métricas de qualidade
{: #anlz_metrics_quality}

Use o monitoramento de qualidade para determinar como o seu modelo prevê resultados. Quando o monitoramento de qualidade é ativado, ele gera um conjunto de métricas a cada hora, por padrão. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.

As métricas de qualidade são calculadas com base nas informações a seguir:

- dados de feedback rotulados manualmente,
- respostas de implementação monitoradas para esses dados.

Para monitoramento adequado, os dados de feedback devem ser registrados no {{site.data.keyword.aios_short}} regularmente. Os dados de feedback podem ser fornecidos usando a opção "Incluir dados de Feedback" ou usando o cliente Python ou a API de REST.

Para mecanismos de aprendizado de máquina diferentes do {{site.data.keyword.aios_short}}, como o Microsoft Azure ML Studio ou o Amazon Sagemaker ML, o monitoramento de qualidade cria solicitações de pontuação adicionais na implementação monitorada.
{: note}

É possível revisar todos os valores de métricas ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de métricas de qualidade que mostra drift de área sob ROC](images/quality_metrics_001.png)


Para revisar detalhes relacionados, como matriz de confusão para classificação binária e de várias classes, que estão disponíveis para algumas métricas, clique no gráfico.

![tabela detalhada de métricas de qualidade](images/quality_metrics_002.png)

### Métricas de qualidade suportadas
{: #anlz_metrics_supqualdets}

As métricas de qualidade a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

#### Área sob ROC
{: #anlz_metrics_supqualdets_roc}

- **Descrição**: área sob rechamada e curva de taxa de falso positivo
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Área sob PR
{: #anlz_metrics_supqualdets_pr}

- **Descrição**: área sob a curva de precisão e rechamada
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Variação explicada da proporção
{: #anlz_metrics_supqualdets_var}

- **Descrição**: a variância explicada da proporção é a proporção de variação explicada e a variação de destino. A variação explicada é a diferença entre a variância de destino e a variância do erro de predição.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

#### Erro médio absoluto
{: #anlz_metrics_supqualdets_abserror}

- **Descrição**: média de diferença absoluta entre a previsão do modelo e o valor de destino
- **Limites padrão**: limite superior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

#### Erro quadrático médio
{: #anlz_metrics_supqualdets_squerror}

- **Descrição**: média de diferença quadrática entre predição de modelo e valor de destino
- **Limites padrão**: limite superior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

#### R ao quadrado
{: #anlz_metrics_supqualdets_r_squared}

- **Descrição**: proporção de diferença entre a variação de destino e a variação para o erro de predição para a variação de destino
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

#### Raiz do erro quadrático médio
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Descrição**: raiz quadrada da média da diferença quadrática entre a predição do modelo e o valor de destino
- **Limites padrão**: limite superior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

#### Precisão
{: #anlz_metrics_supqualdets_acc}

- **Descrição**: a proporção de predições corretas
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipos de problemas**: classificação binária e classificação de classe múltipla
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Taxa positiva verdadeira ponderada (wTPR)
{: #anlz_metrics_supqualdets_wtpr}

- **Descrição**: média ponderada da classe TPR com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Taxa verdadeira positiva (TPR)
{: #anlz_metrics_supqualdets_tpr}

- **Descrição**: proporção de previsões corretas em predições de classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Taxa de falso positivo ponderada (wFPR)
{: #anlz_metrics_supqualdets_wfpr_weighted}

- **Descrição**: média ponderada da classe FPR com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Taxa de falso positivo (FPR)
{: #anlz_metrics_supqualdets_fpr_false}

- **Descrição**: proporção de predições incorretas na classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Rechamada ponderada
{: #anlz_metrics_supqualdets_weighted_recall}

- **Descrição**: média ponderada de rechamada com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Rechamada
{: #anlz_metrics_supqualdets_recall}

- **Descrição**: proporção de predições corretas na classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Precisão ponderada
{: #anlz_metrics_supqualdets_wgth_prec}

- **Descrição**: média ponderada de precisão com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Precisão
{: #anlz_metrics_supqualdets_precision}

- **Descrição**: proporção de previsões corretas em predições de classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Medida F1 ponderada
{: #anlz_metrics_supqualdets_wght_f1-measure}

- **Descrição**: média ponderada de medida F1 com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Medida F1
{: #anlz_metrics_supqualdets_f1-measr}

- **Descrição**: média harmônica de precisão e rechamada
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

#### Perda logarítmica
{: #anlz_metrics_supqualdets_log_loss}

- **Descrição**: média de probabilidades da classe de destino de logaritmos (confiança). Ela também é conhecida como log da verossimilhança esperada.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária e classificação multiclasse
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

### Detalhes de qualidade suportados
{: #anlz_metrics_supqualdets_suppr_dets}

Os detalhes a seguir para as métricas de qualidade são suportados pelo {{site.data.keyword.aios_short}}:

#### Matriz de confusão
{: #anlz_metrics_supqualdets_confusion}

A matriz de confusão ajuda você a entender para qual de seus dados de feedback a resposta de implementação monitorada está correta e para a qual ela não está.

## Métricas de desempenho
{: #anlz_metrics_performance}

Use o monitoramento de desempenho para saber a velocidade dos registros de dados processados por sua implementação. Você ativa o monitoramento de desempenho ao selecionar a implementação a ser rastreada e monitorada pelo {{site.data.keyword.aios_short}}.

As métricas de desempenho são calculadas com base nas informações a seguir:

- dados de carga útil de pontuação

Para o propósito de monitoramento adequado, cada solicitação de pontuação também deve ser
registrada no {{site.data.keyword.aios_short}}. A criação de log de dados de carga útil é automatizada para mecanismos do {{site.data.keyword.pm_full}}. Para outros mecanismos de aprendizado de máquina, os dados de carga útil podem ser fornecidos usando o cliente Python ou a API de REST. O monitoramento de desempenho não cria nenhuma solicitação de pontuação adicional na implementação monitorada.

É possível revisar o valor das métricas de desempenho ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de desempenho](images/performance_metrics_001.png)

### Métricas de desempenho suportadas
{: #anlz_metrics_performance_supp_quality_mets}

As métricas de desempenho a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

#### Rendimento
{: #anlz_metrics_performance_supp_quality_mets_through}

- **Descrição**: média de solicitações de pontuação por minuto em um intervalo de tempo específico
- **Limites padrão**: não aplicável
- **Recomendação padrão**: não aplicável
- **Tipo de problema**: todos
- **Valores de gráfico**: valor médio no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Analítica de dados de carga útil
{: #anlz_metrics_payload}

É possível analisar a carga útil de pontuação que é enviada para sua implementação no intervalo de dados selecionado por um dos métodos a seguir:

- revise as classes de predição e a distribuição de confiança em cada classe
   
   ![um gráfico que mapeia a predição por distribuição de confiança](images/by_confidence.png)
   
- Por gráfico customizado (seleção entre recursos, classes de predição e confiança)
   
   ![um gráfico que mostra o recurso predição para sexo pelo recurso idade](images/by_custom_chart.png)

