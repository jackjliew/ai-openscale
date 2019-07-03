---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: release notes, what's new 

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

# O quê há de novo
{: #rn-relnotes}

Este documento descreve novos recursos para o {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 11 de junho de 2019
{: #rn-11June2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

- __*Funcionalidade do painel atualizado*__: o Painel do {{site.data.keyword.aios_short}} foi submetido a várias revisões. Esta nova versão contém as melhorias a seguir:

    - Um novo painel de ajuda facilita a localização de recursos, como StackOverflow, Suporte IBM e 
    - A globalização foi ativada para o painel
    - Aprimoramentos de usabilidade

## 7 de junho de 2019
{: #rn-7June2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

- __*Interface da linha de comandos aprimorada*__: a interface da linha de comandos, ibm-ai-openscale-cli, foi atualizada e a versão 0.2.148 está liberada agora. Esta nova versão contém as melhorias a seguir:

    - Atualizado o histórico de métricas de qualidade para incluir o intervalo integral de novas métricas de qualidade suportadas pelo OpenScale
    - Suporte para a especificação de um certificado SSL diretamente ao usar o IBM DB2
    - Suporte para o novo SDK do Python ibm-ai-openscale 2.1.8
    - Outras correções de erro e melhorias de estabilidade

   Instale por meio do PyPI executando o comando `pip install -U ibm-ai-openscale-cli` e obtenha a ajuda de uso executando o comando `ibm-ai-openscale-cli --help`. Para obter mais informações, consulte a [página do projeto PyPI](https://pypi.org/project/ibm-ai-openscale-cli).

## 29 de maio de 2019
{: #rn-29May2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

- __*Aprimoramentos de visualização de propensão*__: ![tag beta](images/beta.png) A visualização de propensão inclui as seguintes visualizações: 

    - Carga útil + Perturbado: inclui a solicitação de pontuação recebida para a hora selecionada mais os registros adicionais das horas anteriores se o número mínimo de registros necessários para avaliação não é atendido. Inclui registros adicionais perturbados/sintetizados usados para testar a resposta do modelo quando o valor do recurso monitorado é mudado.
    - Carga útil: as solicitações de pontuação reais recebidas pelo modelo para a hora selecionada.
    - Treinamento: os registros de dados de treinamento usados para treinar o modelo.
    - Sem propensão: a saída do algoritmo sem propensão após o processamento do tempo de execução e de dados perturbados.

   Para obter mais informações, consulte [Visualização de propensão](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Cálculo de precisão para saída sem propensão*__: o Cálculo de precisão inclui saída sem propensão. É possível comparar a precisão do modelo sem propensão com a precisão de um modelo de produção

   Para obter mais informações, consulte [Precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Suporte para múltiplos mecanismos de aprendizado de máquina*__: o {{site.data.keyword.aios_short}} suporta múltiplos mecanismos de aprendizado de máquina em uma única instância, desde que o provisionamento seja executado por meio do [SDK do Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).

   Para obter mais informações, consulte [Suporte para múltiplos mecanismos de aprendizado de máquina](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng).

- __*Suporte de internacionalização*__: o {{site.data.keyword.aios_short}} suporta versões localizadas e inclui dados de processamento em idiomas suportados. A interface com o usuário do {{site.data.keyword.aios_short}}, a documentação e as mensagens de erro estão atualmente traduzidas para os idiomas a seguir: 
    - Alemão
    - Francês
    - Italiano
    - Espanhol
    - Português do Brasil
    - Japonês
    - Chinês simplificado
    - Chinês tradicional
    - Coreano

   Para obter informações adicionais (incluindo limitações), consulte [Idiomas suportados para o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __*Aprimoramentos de estrutura do {{site.data.keyword.pm_full}}*__: o {{site.data.keyword.aios_short}} agora suporta os quadros scikit-learn e XGBoost no mecanismo do {{site.data.keyword.pm_full}}.

   Para obter mais informações, consulte [Estruturas do {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25 de abril de 2019
{: #rn-25April2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

Além de melhorias de usabilidade e atualizações de segurança, nossos desenvolvedores têm estado ocupados com novos recursos. Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados durante as semanas anteriores incluem:

- __*Tour de configuração automatizada*__: uma nova maneira guiada de para configurar seu ambiente do {{site.data.keyword.aios_short}}. Use a [Configuração automatizada](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)
para fornecer serviços, fazer download e configurar um modelo. Você perceberá essa opção quando tiver
uma nova instância do {{site.data.keyword.aios_short}}.
- __*Alternar para beta*__: ![beta tag](images/beta.png) Uma nova alternância, **Explorar a nova versão beta**, permite que você trabalhe em nosso ambiente beta, em que é possível verificar todos os recursos mais recentes e a nova funcionalidade. Não gosta do que vê? Apenas alterne de volta clicando em **Voltar para a versão original**. Sua configuração e monitores não são afetados. Os recursos a seguir fazem parte do programa beta atual:
    - __*Matriz de confusão*__: uma [matriz de confusão exibe](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx) os falsos positivos e os falsos negativos. Clique em uma célula
para visualizar o subconjunto de registros de feedback.

## 10 de abril de 2019
{: #rn-10April2019}

- __*A ferramenta Express Path agora suporta modelos de clientes*__: automatiza o processo de integração ao {{site.data.keyword.aios_short}}.

   Para obter mais informações, consulte [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/).


## 5 de Março de 2019
{: #rn-5March2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Novo modelo Risco de crédito*__: um novo exemplo/tutorial do modelo Risco de crédito é suportado para todos os mecanismos de pontuação. Para obter mais informações, consulte os tópicos [Introdução](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted) e [Recursos adicionais](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov).

- __*Despropensão de cálculo*__: é possível alternar entre o seu modelo de produção e um modelo despropenso criado pelo {{site.data.keyword.aios_short}}. Consulte [Modelo de produção e modelo com a propensão removida](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) e [Entendendo como a remoção da propensão funciona](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) para obter mais informações.

## 22 de fevereiro de 2019
{: #rn-22February2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Atualizações de IU*__: é possível importar um arquivo JSON para configurar programaticamente todos os monitores e recursos durante a criação da assinatura. Também é possível exportar o arquivo de configuração. Consulte o tópico [Configurar assinatura de implementação usando arquivos JSON](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) para obter mais informações.

## 7 de Fevereiro de 2019
{: #rn-7February2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação anterior incluem:

- __*Atualizações de IU*__: várias melhorias foram feitas na interface com o usuário do {{site.data.keyword.aios_short}}, incluindo uma maneira de [verificar a justiça e a precisão on demand](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep) e a capacidade de ver uma lista de transações por meio do [gráfico de detalhes de justiça](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Aprimoramentos de explicabilidade*__: todos os números têm agora a mesma precisão/escala em valores Pertinent Positive (PP) e Pertinent Negative (PN).

- __*Suporte a SSL do Db2*__: o {{site.data.keyword.aios_short}} suporta a aprovação de certificados autoassinados (codificados em Base-64) com credenciais do DB2.

- __*Suporte ao banco de dados do {{site.data.keyword.Bluemix}}*__: o {{site.data.keyword.aios_short}} suporta agora o Databases for PostgreSQL, além do Compose for PostgreSQL e Db2)

## 14 de dezembro de 2018
{: #rn-14December2018}

Os novos recursos, mudanças e problemas conhecidos a seguir com o serviço estão disponíveis.

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação beta incluem:

- __*Disponibilidade geral*__: a liberação de Disponibilidade Geral (GA) do {{site.data.keyword.aios_full_notm}} como um plano Padrão (pago) do {{site.data.keyword.Bluemix}}.

- __*IBM Cloud Pak for Data V1.2*__: se você estiver usando o {{site.data.keyword.wos4d_full}} V1.2, consulte a documentação, incluindo as instruções de instalação, aqui: [Lista de verificação da instalação](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Suporte para seu tipo de modelo*__: além das implementações de modelo de IA no {{site.data.keyword.pm_full}}, o {{site.data.keyword.aios_short}} suporta implementações de modelo no Microsoft Azure, Amazon SageMaker e em ambientes Customizados. Consulte [Tipos de modelo suportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov) para obter mais informações.

- __*Banco de dados "lite" grátis*__: um banco de dados gerenciado "lite" grátis fornece tudo o que você precisa para começar a usar o {{site.data.keyword.aios_short}}. Consulte os [Planos de precificação do {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} para obter detalhes.

- __*Monitoramento de propensão*__: suporte para os atributos protegidos do tipo `float` e `double` e a detecção de propensão em modelos de regressão linear. Além disso, o {{site.data.keyword.aios_short}} pode fazer automaticamente a despropensão de seu modelo IA. Consulte [Entendendo a justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) para obter mais informações.

- __*Explicabilidade*__: suporte para modelos de regressão, funções Python e explicações contrastantes complementares. Consulte [Monitorando explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) para obter mais informações.

- __*Armazenamento de dados*__: monitoramento de qualidade sem reliance no {{site.data.keyword.pm_full}} e a capacidade de usar seu próprio banco de dados, seja Db2, Postgres ou Db2 on Cloud.

- __*IU aprimorada*__: a IU do {{site.data.keyword.aios_short}} foi melhorada para incluir uma distribuição de histograma de tempo de execução com alternância para dados de treinamento, ID do modelo e Versão e uma tabela de ID de transação do histograma. Consulte [Visualizando dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obter mais informações.

- __*Opção de configuração de tutorial alternativo*__: para automatizar o provisionamento e a configuração dos serviços {{site.data.keyword.Bluemix}} necessários e para ver um aplicativo IBM {{site.data.keyword.aios_full}}, incluindo dados de amostra, é possível instalar e executar um módulo Python. Consulte [Instalando um módulo Python para configurar o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 de Setembro de 2018
{: #rn-17September2018}

- **Liberação da visualização beta** - bem-vindo à liberação da visualização beta do {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Próximos passos
{: #relnotes-in-next}

Você ainda tem dúvidas?

- [Limitações](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Problemas Conhecidos](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
