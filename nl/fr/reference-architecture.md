---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Architecture 
{: #architecture}

## Réplication

Un service {{site.data.keyword.composeForEtcd_full}} se compose de trois membres de données etcd dans un cluster, leur espace disque étant réparti dans les zones de disponibilité de la région et vos données répliquées dans les trois membres. Dans un cluster etcd, chaque membre connaît tous les autres membres et repose sur un protocole de consensus réparti pour déterminer le membre leader. Le leader diffuse son statut de leader à intervalle défini. Les suiveurs, en l'absence d'événement provenant du leader, tentent de prendre la place de leader à intervalle également défini. Lorsqu'un membre de données n'est plus accessible, votre cluster continue à fonctionner normalement.

## Chiffrement de disque

Tous les services {{site.data.keyword.composeForEtcd}} disposent du chiffrement au repos. Vos données résident sur des serveurs où le chiffrement au niveau volume est activé. 

Etant donné que {{site.data.keyword.composeForEtcd}} est un service géré, les opérateurs {{site.data.keyword.cloud}} Compose peuvent voir les données. Outre le chiffrement du disque, vous devez chiffrer vos informations personnelles avant de les stocker dans la base de données ou utiliser des extensions ou des fonctions permettant d'activer le chiffrement sur la base de données elle-même. Même si ces méthodes risquent d'avoir un impact sur la facilité d'utilisation ou les performances, il est conseillé de s'assurer que les informations personnelles sont protégées par un chiffrement.

## Mise à l'échelle automatique

Les ressources sont automatiquement mises à l'échelle en fonction de l'utilisation totale de la mémoire des bases de données etcd. Le stockage est basé sur un rapport de mise à disposition de mémoire RAM de 4 sur 1. Ces ressources sont intégrées en tant qu'unités.

La mise à l'échelle automatique est conçue pour répondre aux tendances à court et moyen termes de votre base de données. Votre service est contrôlé toutes les minutes et, s'il est à court de mémoire RAM, des unités supplémentaires sont attribuées au déploiement. 

Une mise à l'échelle automatique ne réduit pas la taille des déploiements où l'utilisation du disque/de la mémoire à diminué. Les ressources mises à disposition de vos bases de données sont conservées pour les besoins ultérieurs ou jusqu'à ce que vous réduisiez manuellement votre déploiement.
{: .tip}
