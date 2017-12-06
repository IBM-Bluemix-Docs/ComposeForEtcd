---

copyright:
  years: 2016,2017
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd est un espace de stockage de paires clé-valeur contenant les données toujours correctes dont vous avez besoin afin de coordonner et gérer votre cluster de serveurs pour la gestion des configurations de serveur distribué. etcd utilise l'algorithme de consensus RAFT pour garantir la cohérence des données dans votre cluster. Il impose l'ordre dans lequel les opérations sont exécutées sur les données de manière à obtenir les mêmes résultats et de la même façon pour chaque noeud du cluster. {{site.data.keyword.composeForEtcd_full}} ajoute des sauvegardes automatiques des données de configuration stockées dans etcd. Une interface d'administration intuitive vous permet de surveiller, de mettre à l'échelle et d'administrer votre déploiement avec beaucoup plus de facilité.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte {{site.data.keyword.cloud}}.

## Création d'une instance de service Compose for Etcd

[Créez une instance {{site.data.keyword.composeForEtcd_full}}](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

Lorsque vous mettez votre instance {{site.data.keyword.composeForEtcd}} à disposition, vous avez le choix entre le plan *Standard* et le plan *Entreprise*. Avec le plan *Entreprise*, vous pouvez mettre votre instance {{site.data.keyword.composeForEtcd}} à disposition dans un cluster {{site.data.keyword.composeEnterprise}} disponible. {{site.data.keyword.composeEnterprise}} fournit la sécurité et l'isolement requis par les normes de conformité des entreprises et utilise un réseau dédié pour garantir les performances des bases de données déployées. Pour plus d'informations, voir la [documentation Compose - Entreprise](../ComposeEnterprise/index.html).

## Gestion de Compose for Etcd

Vous pouvez gérer votre service depuis son tableau de bord. Vous y trouverez des informations concernant la base de données Compose d'{{site.data.keyword.cloud_notm}} et la manière de vous y connecter. Vous pouvez également :
- gérer vos sauvegardes ;
- allouer plus de ressources à votre service ;
- modifier le mot de passe du service ;
- constituer des listes blanches pour limiter l'accès à vos bases de données.
Pour plus d'informations, voir [Paramètres](./dashboard-settings.html).

## Connexion à Compose for Etcd

Vous pouvez vous connecter à votre service avec les données d'identification créées en même temps que le service ou avec les chaînes de connexion et la ligne de commande fournies dans l'onglet *Vue d'ensemble* du tableau de bord de votre service.

## Connexion d'une application {{site.data.keyword.cloud_notm}} à Compose for Etcd

Pour connecter une application {{site.data.keyword.cloud_notm}} à votre service, utilisez les données d'identification créées en même temps que le service. Pour plus d'informations sur la connexion d'une application {{site.data.keyword.cloud_notm}} à un service {{site.data.keyword.composeForEtcd}}, voir [Connexion d'une application {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connexion à Compose for Etcd depuis l'extérieur d'{{site.data.keyword.cloud_notm}}

Pour vous connecter à {{site.data.keyword.composeForEtcd}} depuis l'extérieur d'{{site.data.keyword.cloud_notm}}, vous pouvez utiliser les chaînes de connexion ou la ligne de commande fournies. Pour plus d'informations sur ce type de connexion, voir [Connexion d'une application externe](./connecting-external.html).
