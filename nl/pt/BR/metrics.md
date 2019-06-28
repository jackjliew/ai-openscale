---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Criando monitores e métricas customizados ![tag beta](images/beta.png)
{: #cst_mtrcs}

Os monitores customizados consolidam um conjunto de métricas customizadas que permitem controlar,
de uma maneira quantitativa, qualquer aspecto de sua implementação de modelo e aplicativo de negócios. É
possível definir métricas customizadas e usá-las junto com as métricas padrão, tais como a qualidade do
modelo, o desempenho ou as métricas de justiça que são monitoradas no {{site.data.keyword.aios_full}}.
{: shortdesc}

Para gerenciar monitores e métricas customizados, deve-se usar a interface programática que faz
parte do SDK Python. De maneira semelhante, é possível armazenar métricas customizadas no data mart do {{site.data.keyword.aios_short}} para acessá-las quando necessário. Métricas customizadas também
são visualizadas no {{site.data.keyword.aios_short}} Dashboard.

## Gerenciando métricas customizadas
{: #cst_mtrc_mgmt}

Para trabalhar com métricas customizadas, deve-se executar as tarefas a seguir:

1. Registre o monitor customizado com a definição de métricas.
2. Ative o monitor customizado.
3. Armazene os valores das métricas.

Os tutoriais avançados a seguir mostram como fazer isso:

- [Trabalhando com o Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Trabalhando com o mecanismo de aprendizado de máquina customizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

É possível desativar e ativar novamente o monitoramento customizado a qualquer momento. Você poderá
remover o monitor customizado se não precisar mais dele.

Para obter mais informações, veja a [documentação
do SDK Python](http://ai-openscale-python-client.mybluemix.net/).

## Acessando e visualizando métricas customizadas
{: #cst_mtrcs_viz}

Para acessar e visualizar métricas customizadas, é possível usar a interface programática. Os tutoriais avançados a seguir mostram como fazer isso:

- [Trabalhando com o Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [Trabalhando com o mecanismo de aprendizado de máquina customizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   Para obter mais informações, veja [a documentação do SDK Python](http://ai-openscale-python-client.mybluemix.net/).

A visualização de suas métricas customizadas é exibida no {{site.data.keyword.aios_short}} Dashboard.

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
