---
copyright:
  years: 2016,2018
lastupdated: "2018-06-11"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuration de connexion
{: #connection-configuration}

Les connexions à la base de données {{site.data.keyword.composeForEtcd_full}} sont gérées par 2 portails HAProxy. Chaque portail dispose de 64 Mo de mémoire.

Disposer de deux portails permet aux applications de conserver une connectivité lorsque l'un des portails n'est plus accessible. Le basculement côté client relève de la responsabilité du concepteur d'applications. Certains pilotes etcd gèrent automatiquement plusieurs chaînes de connexion et le basculement sans perte de données. Si vous ne travaillez pas avec un pilote qui gère totalement les erreurs de basculement, procédez comme suit pour gérer vous-même les erreurs.

* Utilisez un pilote qui accepte plusieurs noeuds finaux dans sa configuration de connexion.
* Vérifiez que les appels de vos application's en vue d'une lecture ou d'une écriture dans la base de données réagissent aux erreurs de manière appropriée. Vous pouvez configurer votre application pour réagir aux erreurs de différentes manières, notamment :
  - Consignation de l'erreur et reconnexion.
  - Reconnexion et nouvel essai de l'opération à l'origine de l'erreur.
  - Mise en file d'attente de l'opération ayant échoué et planification d'une reconnexion.

## Chiffrement du transport

Tous les portails {{site.data.keyword.composeForEtcd}} HAProxy disposent de TLS/SSL et prennent en charge TLS version 1.2. Les certificats du service sont des certificats Let's Encrypt.

## Limites de connexion

Les connexions de base de données sont limitées à 2000 connexions par portail. Lorsque la limite de connexion est dépassée, le service ne répond plus. Vous pouvez gérer les connexions à partir de votre application à l'aide de la fonction de regroupement de connexions de votre pilote.

## Délais d'attente de proxy

Les portails HAProxy gèrent le cycle de vie des connexions entre le serveur et le client. Nous en fournissons le détail à titre de référence pour les éditeurs de routeurs et les personnes intéressées par les activités de bas niveau des connexions de base de données {{site.data.keyword.composeForEtcd}}.

Paramètre | Valeur | S'applique
----------|-----------|-----------
client | 1 jour | Lorsque le client doit accuser réception de données ou en envoyer.
connect | 1m | Lorsqu'une connexion est établie entre le proxy et le serveur.
server | 1 jour | Lorsque le serveur doit accuser réception de données ou en envoyer.
check | 1m | En tant que vérification secondaire du délai d'attente lorsqu'une connexion est établie entre le proxy et le serveur.
{: caption="Tableau 1. Délais d'attente des portails HAProxy etcd" caption-side="top"}
