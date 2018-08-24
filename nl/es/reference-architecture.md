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

# Arquitectura 
{: #architecture}

## Réplica

Un servicio de {{site.data.keyword.composeForEtcd_full}} contiene tres miembros de datos etcd en un clúster, con su espacio de disco dispersado por las zonas de disponibilidad de la región y los datos replicados en los tres. En un clúster de etcd, cada miembro conoce a todos los miembros y se basa en un protocolo de consenso distribuido para determinar el líder. El líder difunde su estado de líder en un intervalo establecido. Los seguidores, si no se ha recibido nada del líder, todos tienen su propio intervalo tras el cual intentarán convertirse en un líder. Si un miembro de datos se vuelve inalcanzable, el clúster continúa operando con normalidad.

## Cifrado de disco

Todos los servicios de {{site.data.keyword.composeForEtcd}} tienen cifrado en reposo. Los datos residen en servidores que tienen el cifrado de nivel de volumen habilitado. 

Puesto que {{site.data.keyword.composeForEtcd}} es un servicio gestionado, es posible que los operadores de {{site.data.keyword.cloud}} Compose vean los datos. Además del cifrado de disco, debe cifrar información personal antes de almacenarla en la base de datos o utilizar extensiones o características para habilitar el cifrado en la propia base de datos. Si bien estos métodos pueden afectar a la usabilidad o al rendimiento, es una buena práctica asegurarse de que la información personal esté protegida con cifrado.

## Escalado automático

Los recursos se escalan automáticamente basándose en el uso de memoria total de las bases de datos etcd. El almacenamiento se basa en una proporción de RAM suministrada de 4:1. Estos recursos se empaquetan como unidades.

El escalado automático está diseñado para responder a las tendencias a corto y medio plazo de la base de datos. Cada minuto, el servicio está marcado y si se está quedando corto en RAM, se asignan más unidades al despliegue. 

El escalado automático no reduce los despliegues en los que el uso de disco/memoria se ha reducido. Los recursos suministrados a las bases de datos se conservan para sus necesidades futuras, o hasta que reduzca manualmente el despliegue.
{: .tip}
