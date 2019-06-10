---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: release notes, what's new 

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

# O quê há de novo
{: #rn-relnotes}

Este documento descreve novos recursos para o {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 29 de maio de 2019
{: #rn-29May2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

- __*Aprimoramentos de visualização de propensão*__: ![tag beta](images/beta.png) A visualização de propensão inclui as seguintes visualizações: 

    - Carga útil + Perturbado: inclui a solicitação de pontuação recebida para a hora selecionada mais os registros adicionais das horas anteriores se o número mínimo de registros necessários para avaliação não é atendido. Inclui registros adicionais perturbados/sintetizados
usados para testar a resposta do modelo quando o valor do recurso monitorado muda.
    - Carga útil: as solicitações de pontuação reais recebidas pelo modelo para a hora selecionada.
    - Treinamento: os registros de dados de treinamento usados para treinar o modelo.
    - Sem propensão: a saída do algoritmo sem propensão após o processamento do tempo de execução e de dados perturbados.

   Para obter mais informações, consulte [Visualização de propensão](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz).

- __*Cálculo de precisão para saída sem propensão*__: o Cálculo de precisão inclui saída sem propensão. É possível comparar a precisão do modelo sem propensão com a precisão de um modelo de produção

   Para obter mais informações, consulte [Precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view).

- __*Suporte para vários mecanismos de aprendizado de máquina*__: o {{site.data.keyword.aios_short}} suporta vários mecanismos de aprendizado de máquina em uma única instância, desde que o fornecimento seja executado por meio da interface da linha de comandos (CLI).

   Para obter mais informações, consulte [Ferramenta CLI do ModelOps](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mop).

- __*Suporte de internacionalização*__: o {{site.data.keyword.aios_short}} suporta versões localizadas e inclui dados de processamento em idiomas suportados. A interface com o usuário do {{site.data.keyword.aios_short}}, a documentação e as mensagens de erro estão atualmente traduzidas para os idiomas a seguir: 
    - German
    - French
    - MQCO_NONE
    - espanhol
    - Português do Brasil
    - japonês
    - Chines Simplificado
    - chinês tradicional
    - PC5250 Chinês Tradicional

   Para obter informações adicionais (incluindo limitações), consulte [Idiomas suportados para o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-sl-langs).

- __*Aprimoramentos de estrutura do {{site.data.keyword.pm_full}}*__: o {{site.data.keyword.aios_short}} agora suporta os quadros scikit-learn e XGBoost no mecanismo do {{site.data.keyword.pm_full}}.

   Para obter mais informações, consulte [Estruturas WML](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml).

## 25 de abril de 2019
{: #rn-25April2019}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

Além de melhorias de usabilidade e atualizações de segurança, nossos desenvolvedores têm estado ocupados com novos recursos. Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados durante as semanas anteriores incluem:

- __*Tour de configuração automatizada*__: uma nova maneira guiada de para configurar seu ambiente do {{site.data.keyword.aios_short}}. Use a [Configuração automatizada](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)
para fornecer serviços, fazer download e configurar um modelo. Você perceberá essa opção quando tiver
uma nova instância do {{site.data.keyword.aios_short}}.
- __*Alternar para beta*__: ![tag beta](images/beta.png) uma nova alternância, **Explorar a nova versão beta**, permite que você
trabalhe em nosso ambiente beta, no qual é possível verificar todos os recursos mais recentes e as novas funcionalidades. Não gosta do que vê? Somente alterne de volta clicando em **Voltar para a versão original**. A configuração e os monitores não são afetados. Os recursos a seguir fazem parte do
programa beta atual:
    - __*Matriz de confusão*__: uma [matriz de confusão exibe](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx#it-conf-mtx) os falsos positivos e os falsos negativos. Clique em uma célula
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

- __*Despropensão de cálculo*__: é possível alternar entre o seu modelo de produção e um modelo despropenso criado pelo {{site.data.keyword.aios_short}}. Consulte [Modelo de produção e modelo despropenso](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb) e [Entendendo como a despropensão funciona](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) para obter mais informações.

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

- __*Suporte ao IBM Cloud Database*__: o {{site.data.keyword.aios_short}} suporta agora o Databases for PostgreSQL, além do Compose for PostgreSQL e Db2)

## 14 de dezembro de 2018
{: #rn-14December2018}

Os novos recursos, mudanças e problemas conhecidos a seguir com o serviço estão disponíveis.

Os recursos do {{site.data.keyword.aios_short}} que foram incluídos ou aprimorados desde a liberação beta incluem:

- __*Disponibilidade geral*__: a liberação de Disponibilidade Geral (GA) do {{site.data.keyword.aios_full_notm}} como um plano IBM Cloud Standard (pago).

- __*IBM Cloud Private for Data V1.2*__: se você estiver usando o {{site.data.keyword.aios_short}} no IBM Cloud Private for Data V1.2, consulte a documentação, incluindo as instruções de instalação, aqui: [Lista de verificação da instalação](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*Suporte para seu tipo de modelo*__: além das implementações de modelo IA no Watson Machine Learning, o {{site.data.keyword.aios_short}} suporta implementações de modelo no Microsoft Azure, Amazon SageMaker e em ambientes Customizados. Consulte [Tipos de modelo suportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov) para obter mais informações.

- __*Banco de dados "lite" grátis*__: um banco de dados gerenciado "lite" grátis fornece tudo o que você precisa para começar a usar o {{site.data.keyword.aios_short}}. Consulte os [Planos de precificação do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/watson-openscale){: new_window} para obter detalhes.

- __*Monitoramento de propensão*__: suporte para os atributos protegidos do tipo `float` e `double` e a detecção de propensão em modelos de regressão linear. Além disso, o {{site.data.keyword.aios_short}} pode fazer automaticamente a despropensão de seu modelo IA. Consulte [Entendendo a justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor) para obter mais informações.

- __*Explicabilidade*__: suporte para modelos de regressão, funções Python e explicações contrastantes complementares. Consulte [Monitorando explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov) para obter mais informações.

- __*Armazenamento de dados*__: o monitoramento de qualidade sem reliance no Watson Machine Learning e a capacidade de usar seu próprio banco de dados, seja Db2, Postgres ou Db2 on Cloud.

- __*IU aprimorada*__: a IU do {{site.data.keyword.aios_short}} foi melhorada para incluir uma distribuição de histograma de tempo de execução com alternância para dados de treinamento, ID do modelo e Versão e uma tabela de ID de transação do histograma. Consulte [Visualizando dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) para obter mais informações.

- __*Opção de configuração de tutorial alternativo*__: para automatizar o fornecimento e a configuração dos serviços necessários do IBM Cloud e para ver um aplicativo IBM {{site.data.keyword.aios_full}}, incluindo dados de amostra, é possível instalar e executar um módulo Python. Consulte [Instalando um módulo Python para configurar o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 17 de Setembro de 2018
{: #rn-17September2018}

- **Liberação da visualização beta** - bem-vindo à liberação da visualização beta do {{site.data.keyword.aios_full_notm}}.

<p>&nbsp;</p>

## Próximos passos
{: #relnotes-in-next}

Você ainda tem dúvidas?

- [Limitações](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [Problemas Conhecidos](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
