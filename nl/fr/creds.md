---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Création d'identifiants
{: #cred-create}

Pour accéder aux API {{site.data.keyword.aios_short}} REST, il faut une clé d'API de plateforme et un ID de magasin de données (d'instance de service).
La clé d'API de plateforme donne à un utilisateur la possibilité d'accéder aux ressources {{site.data.keyword.cloud_notm}}.

Pour les comptes d'entreprise,
un administrateur peut créer le magasin de données puis inviter les autres utilisateurs dans le compte
en leur donnant l'accès à un magasin de données {{site.data.keyword.aios_short}} spécifique.
Chaque utilisateur peut alors créer sa propre clé d'API de plateforme et accéder au même magasin de données {{site.data.keyword.aios_short}} ;
il n'y a aucun risque de conflit ou de sécurité.

Pour créer une clé d'API de plateforme, procédez comme suit :

- Connectez-vous à
[{{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}.

- Sélectionnez **Gérer** --> **Sécurité** --> **Clés d'API de plateforme**

    ![Clés d'API de plateforme](images/cred-api-key.png)

- Créez et enregistrez une clé d'API de plateforme.

Pour trouver votre ID de magasin de données (ou d'instance de service) :

- Sur la page {{site.data.keyword.aios_short}} **Configuration --> Récapitulatif**,
la première entrée est votre ID de magasin de données (ou d'instance de service).

    ![ID de magasin de données](images/data-mart-id.png)
