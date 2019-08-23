---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# Haute disponibilité et reprise après incident
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} est à haute disponibilité sur plusieurs sites {{site.data.keyword.cloud_notm}}, tels que Dallas et Washington. Toutefois, la reprise après un incident potentiel affectant tout un site nécessite une planification et une préparation.
{: shortdesc}

Vous êtes tenu de comprendre votre configuration, votre personnalisation et votre utilisation du service. Vous êtes également tenu d'être prêt à recréer une instance du service sur un nouveau site et à restaurer vos données sur n'importe quel site. Pour plus d'informations, consultez [Comment garantir zéro indisponibilité ?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external}.

## Haute disponibilité 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} est déployé et disponible dans les data centers
**us-south** avec un routage MZR (multiple zone routing) sur trois zones de disponibilité. À tout moment, si une zone n'est pas disponible, le système reste disponible dans les autres zones de disponibilité. L'équilibreur de charge globale et le serveur DNS routent le trafic vers les zones disponibles sans aucune interruption pour les utilisateurs.

Les données stockées dans les bases de données PostgreSQL sont également à haute disponibilité et se trouvent dans plusieurs zones de disponibilité. Le client doit toutefois sauvegarder ses données dans le cadre d'un plan de reprise après incident pour que les services puissent être recréés.

Le trafic {{site.data.keyword.aios_short}} fait l'objet d'un équilibrage de charge entre plusieurs zones dans une région. Chaque zone est un data center de la même région. 

Les bases de données Compose, comme les bases de données PostgreSQL et etcd (<code>etc</code> directory) réparties,
sont sauvegardées périodiquement pour garantir la haute disponibilité et, en cas d'incident,
l'équipe d'exploitation {{site.data.keyword.aios_short}} sera en mesure de restaurer le service dans le délai RPO (Recovery Point Objective).
 
{{site.data.keyword.cloud_notm}} offre une redondance des données dans la région qui permet une protection par haute disponibilité. IBM assure une réplication automatique des données pour les bases de données client qui contiennent des données de formation et/ou de modèle personnalisé sans coût supplémentaire. La réplication est effectuée dans les zones de disponibilité de la région dans les data centers {{site.data.keyword.cloud_notm}}.
 
## Sauvegarde et restauration
{: #openscale-restore}

Les clients sont responsables de sauvegarder et de restaurer leurs données,
y compris les données de formation et/ou de modèle personnalisé ainsi que tous les modèles personnalisés générés par eux. Pour les instructions de sauvegarde et de restauration client, consultez la documentation d'{{site.data.keyword.cloud_notm}}.
 
## Reprise après incident
{: #openscale-disaster-recovery}

La continuité des opérations dans une région est assurée en
utilisant la réplication automatique dans les zones de disponibilité de la région dans les data centers {{site.data.keyword.cloud_notm}}. La reprise après incident multi-région relève de la responsabilité du client. Il doit sauvegarder, restaurer et synchroniser
ses politiques de sécurité, ses données de formation et/ou de modèle personnalisé, et tous les modèles personnalisés générés par lui. En outre, le client est responsable du routage et/ou de l'équilibrage de charge entre les régions. Pour les instructions de sauvegarde et de restauration client, consultez la documentation d'{{site.data.keyword.cloud_notm}}.
