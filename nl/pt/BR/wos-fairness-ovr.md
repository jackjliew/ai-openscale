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

# Visão geral das métricas de justiça
{: #anlz_metrics_fairness}

Use o monitoramento de justiça do {{site.data.keyword.aios_full}} para determinar se os resultados produzidos por seu modelo são justos ou não para o grupo monitorado. Quando o monitoramento de justiça está ativado, por padrão, ele
gera um conjunto de métricas a cada hora. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.
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

## Entendendo a Equidade
{: #mf-understand}

O {{site.data.keyword.aios_short}} verifica seu modelo implementado para propensão no tempo de execução. Para detectar a propensão para um modelo implementado, deve-se definir os atributos de justiça, como Idade ou Gênero, conforme detalhado na seção [Configurando o monitor de justiça](#mf-config) a seguir.

É obrigatório especificar o esquema de saída para um modelo ou função no {{site.data.keyword.pm_short}}, para que a verificação de propensão seja ativada no {{site.data.keyword.aios_short}}. O esquema de saída pode ser especificado usando a propriedade `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` na parte de metadados da API `store_model`. Para obter mais informações, consulte a [documentação do cliente {{site.data.keyword.pm_full}}](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### Como ele funciona
{: #mf-works}

Antes de configurar o monitor de Justiça, há alguns conceitos chave que são críticos para entender:

- Os atributos de justiça são os atributos de modelo para os quais o modelo provavelmente exibirá propensão. Como um exemplo, para o atributo de justiça **`Gender`**, o modelo pode ser propenso com relação a valores de gênero específicos (`Female`, `Transgender` etc.) Outro exemplo de um atributo de justiça é **`Age`**, em que o modelo pode exibir propensão com relação a pessoas em um grupo de idade, como `18 to 25`.

- Valores de referência monitorados: os valores de atributos de justiça são divididos em duas categorias distintas: Referência e Monitorado. Os valores Monitorados são aqueles que provavelmente serão discriminados. No caso de um atributo de justiça como **`Gender`**, os valores Monitorados podem ser `Female` e `Transgender`. Para um atributo de justiça numérico, como **`Age`**, os valores Monitorados podem ser `[18-25]`. Todos os outros valores para um determinado atributo de justiça são, então, considerados como valores de Referência, por exemplo, `Gender=Male` ou `Age=[26,100]`.

- Resultados favoráveis e desfavoráveis: a saída do modelo é categorizada como Favorável ou Desfavorável. Como um exemplo, se o modelo estiver prevendo se uma pessoa deve obter um empréstimo ou não, o resultado Favorável poderá ser `Loan Granted` ou `Loan Partially Granted`, enquanto o resultado Desfavorável pode ser `Loan Denied`. Portanto, o resultado Favorável é aquele que é considerado como um resultado positivo, enquanto o resultado Desfavorável é considerado como sendo negativo.

O algoritmo do {{site.data.keyword.aios_short}} calcula a propensão em uma base por hora, usando os últimos `N` registros presentes na tabela de criação de log de carga útil; o valor de `N` é especificado ao configurar a Justiça. O algoritmo perturba esses últimos `N` registros para gerar dados adicionais.

A perturbação é feita mudando o valor do atributo fairness de Reference para Monitored ou vice-versa. Os dados perturbados são então enviados para o modelo para avaliar seu comportamento. O algoritmo examina os últimos `N` registros na tabela de carga útil e o comportamento do modelo nos dados perturbados para decidir se o modelo está agindo de uma maneira propensa.

Um modelo será considerado como propenso se, nesse conjunto de dados combinado, a porcentagem de resultados Favoráveis para a classe Monitorada for menor que a porcentagem de resultados Favoráveis para a classe de Referência, por algum valor do limite. Esse valor do limite deve ser especificado ao configurar a Justiça.

Os valores de justiça podem ser mais de 100%. Isso significa que o grupo Monitorado recebeu resultados mais favoráveis do que o grupo de Referência. Além disso, se nenhuma nova solicitação de escoragem for enviada, o Valor de justiça permanecerá constante.
{: note}

### Fazer os cálculos
{: #mf-bias-math}

A métrica de justiça usada no {{site.data.keyword.aios_short}} é um impacto desproporcional, que é uma medida de como a taxa na qual um grupo não privilegiado recebe um determinado resultado se compara com a taxa na qual um grupo privilegiado recebe esse mesmo resultado.

A fórmula matemática a seguir é usada para calcular o impacto desproporcional:

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
Disparate impact =   ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

em que `num_positives` é o número de indivíduos no grupo (privileged=False, ou seja, não privilegiado, ou privileged=True, ou seja, privilegiado) que recebeu um resultado positivo e num_instances é o número total de indivíduos no grupo.

O número resultante será uma porcentagem, ou seja, a porcentagem de comparação entre a taxa na qual o grupo não privilegiado recebe o resultado positivo e a taxa na qual o grupo privilegiado recebe o resultado positivo. Por exemplo, se um modelo de risco de crédito designar a previsão “sem risco” para 80% de requerentes não privilegiados e para 100% de requerentes privilegiados, esse modelo terá um impacto desproporcional (apresentado como a pontuação de justiça no {{site.data.keyword.aios_short}}) de 80%.

No {{site.data.keyword.aios_short}}, os resultados positivos são designados como os resultados favoráveis e os resultados negativos são designados como os resultados desfavoráveis. O grupo privilegiado é designado como o grupo de referência e o grupo não privilegiado é designado como o grupo monitorado.


### Visualização de propensão ![beta tag](images/beta.png)
{: #mf-monitor-bias-viz}

Quando uma propensão em potencial é detectada, o {{site.data.keyword.aios_short}} executa várias funções para confirmar se a propensão é real. O {{site.data.keyword.aios_short}} perturba os dados invertendo o valor monitorado para o valor de referência e, em seguida, executando esse novo registro por meio do modelo. Em seguida, ele exibe a saída resultante como uma saída sem propensão. O {{site.data.keyword.aios_short}} também treina um modelo sem propensão de sombra que depois é usado para detectar quando um modelo fará uma previsão com propensão. 

Dois conjuntos de dados diferentes são usados para calcular a justiça e a precisão. A justiça é calculada usando a carga útil + os dados perturbados. A precisão é calculada usando os dados de feedback. Para calcular a precisão, o {{site.data.keyword.aios_short}} precisa de dados rotulados manualmente, que estão presentes apenas na tabela de feedback.

Os resultados dessas determinações estão disponíveis na visualização de propensão, que inclui as seguintes visualizações (as visualizações serão exibidas somente se houver dados a serem suportados).

- **Carga útil + Perturbado**: inclui a solicitação de pontuação recebida para a hora selecionada mais os registros adicionais das horas anteriores se o número mínimo de registros necessários para avaliação não é atendido. Inclui registros adicionais perturbados/sintetizados
usados para testar a resposta do modelo quando o valor do recurso monitorado muda.

   Anote as cargas úteis e detalhes perturbados a seguir:

   - número de registros que são lidos nesta hora por meio da tabela de carga útil
   - Registros adicionais que são lidos por meio de horas anteriores (por exemplo, se o valor `min_records` na configuração de justiça for configurado para 1.000 e apenas 10 registros forem incluídos das 14h às 15h, para atender ao requisito mínimo, o sistema lerá um adicional de 990 registros de horas anteriores.)
   - Registros perturbados por atributo de justiça
   - Registro de data e hora mais antigo no quadro de dados para o qual a propensão deve ser calculada
   - O registro de data e hora mais recente/mais novo no quadro de dados para o qual a propensão deve ser calculada

  ![exemplo de carga útil mais perturbados](images/payload&perturbed.png)



- **Carga útil**: as solicitações de pontuação reais recebidas pelo modelo para a hora selecionada.

   Anote os detalhes da carga útil a seguir:
   
   - número de registros que são lidos/em que a operação sem propensão é executada por meio da tabela de carga útil
   - Registro de data e hora mais antigo no quadro de dados para o qual a propensão deve ser calculada
   - O registro de data e hora mais recente/mais novo no quadro de dados para o qual a propensão deve ser calculada


  ![exemplo de dados de carga útil](images/payload.png)

- **Treinamento**: os registros de dados de treinamento usados para treinar o modelo.

   Anote os detalhes de treinamento a seguir:
   
   - número de registros de dados de treinamento. Os dados de treinamento são lidos uma vez e a distribuição é armazenada na variável `subscription/fairness_configuration`. Ao calcular a distribuição, também é necessário encontrar o número de registros de dados de treinamento e armazená-lo na mesma distribuição. Também, quando os dados de treinamento mudarem, ou seja, se o comando `POST /data_distribution` for executado novamente, esse valor será atualizado na variável `fairness_configuration/training_data_distribution`. Ao enviar a métrica, é necessário enviar esse valor também.
   - O horário em que os dados de treinamento são processados pela última vez (primeira vez e atualizações subsequentes)

  ![exemplo de dados de treinamento](images/training.png)
   

   
- **Sem propensão**: a saída do algoritmo sem propensão após o processamento do tempo de execução e de dados perturbados. A seleção do botão de opções **Sem propensão** mostra as mudanças no modelo sem propensão, em comparação com o modelo em produção. O gráfico reflete o status de resultado aprimorado dos grupos.


   Anote os detalhes sem propensão a seguir:
   
   - número de registros que são lidos/nos quais a operação sem propensão é executada por meio da tabela de carga útil
   - Registros adicionais que são lidos para executar propensão e, portanto, sem propensão também. Mesmo número que na seleção `Carga útil + Perturbado`
   - Registros perturbados por atributo de justiça
   - Registro de data e hora mais antigo no quadro de dados para o qual a propensão deve ser calculada
   - O registro de data e hora mais recente/mais novo no quadro de dados para o qual a propensão deve ser calculada
   - O valor de justiça anterior e o posterior são exibidos na parte do cabeçalho da visualização Sem propensão. 
      - A precisão **posterior** é calculada usando os dados de feedback e enviando-os para a API de remoção de propensão ativa. Essa API retorna a predição sem propensão. Os dados de feedback também contêm o rótulo manual. O rótulo manual é comparado com a predição sem propensão para calcular a precisão. Essa API retorna a predição sem propensão. A tabela de feedback também contém o rótulo manual. O rótulo manual é comparado com a predição sem propensão para calcular a precisão. 
      - A precisão **anterior** é calculada usando os mesmos dados de feedback. Para o cálculo de precisão anterior, os dados de feedback são enviados para o modelo para obter sua predição e o valor previsto é comparado com o rótulo manual para obter a precisão.

  ![exemplo de dados sem propensão](images/debiased.png)
  
### Por exemplo
{: #mf-ex1}

Considere um ponto de dados em que, para `Gender=Male` (valor de Referência), o modelo prevê um resultado Favorável, mas quando o registro é perturbado mudando `Gender` para `Female` (valor Monitorado), enquanto mantém todos os outros valores de recurso iguais, o modelo prevê um resultado Desfavorável. Um modelo geral é indicado para exibir propensão se houver pontos de dados suficientes (nos últimos `N` registros na tabela de carga útil, mais os dados perturbados) em que o modelo estava agindo de uma maneira propensa.

### Modelos suportados
{: #mf-supmo}

 O {{site.data.keyword.aios_short}} suporta a detecção de propensão somente para os modelos e funções Python que esperam algum tipo de dados estruturados em seu vetor de recurso.

As métricas de justiça são calculadas com base nas informações a seguir:

- dados de carga útil de pontuação.

Para o propósito de monitoramento adequado, cada solicitação de pontuação também deve ser
registrada no {{site.data.keyword.aios_short}}. A criação de log de dados de carga útil é
automatizada para mecanismos {{site.data.keyword.pm_full}}.

Para outros mecanismos de aprendizado de máquina, os dados de carga útil podem ser fornecidos
usando o cliente Python ou a API de REST.

Para mecanismos de aprendizado de máquina diferentes do {{site.data.keyword.pm_full}},
o monitoramento de justiça cria solicitações de pontuação adicionais na implementação monitorada.
{: note}

É possível revisar todos os valores de métricas ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/fairness_metrics_001.png)

É possível revisar detalhes relacionados, tais como resultados favoráveis e desfavoráveis:

![detalhes de justiça](images/fairness_metrics_002.png)

É possível visualizar transações detalhadas:

![um gráfico de justiça mostrando uma lista de transações](images/fairness_metrics_003.png)

É possível visualizar o terminal de pontuação com propensão reduzida recomendado:

![detalhes do terminal de pontuação com propensão reduzida](images/fairness_metrics_004.png)

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
