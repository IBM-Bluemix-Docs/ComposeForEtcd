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

# Configuración de conexión
{: #connection-configuration}

Las conexiones de base de datos {{site.data.keyword.composeForEtcd_full}} están gestionadas por 2 portales HAProxy. Cada portal tiene 64 MB de memoria.

Los dos portales permiten que las aplicaciones mantengan la conectividad en el caso de que uno de los portales se convierta en no accesible. La migración tras error en el lado del cliente es responsabilidad del diseñador de aplicaciones. Algunos controladores etcd manejan automáticamente varias series de conexión y una migración tras error ordenada. Si no utiliza un controlador que gestione por completo los errores de migración tras error, debe seguir los siguientes pasos para gestionar los errores:

* Utilizar un controlador que acepte varios puntos finales en su configuración de conexión.
* Asegurarse de que las llamadas de su aplicación para leer o escribir en la base de datos reaccionen a los errores adecuadamente. Puede configurar la aplicación para que reaccione a los errores de distintas formas, incluido lo siguiente:
  - Registre el error y vuelva a conectarse.
  - Reconectar y reintentar la operación que ha provocado el error.
  - Poner en cola la operación que ha fallado y planificar la reconexión.

## Cifrado en tránsito

Todos los portales HAProxy de {{site.data.keyword.composeForEtcd}} tienen habilitado TLS/SSL y dan soporte a TLS versión 1.2. Los certificados para el servicio son certificados de Let's Encrypt.

## Límites de conexión

Las conexiones de base de datos tienen un límite de conexión de 2000 conexiones por portal. El exceso del límite de conexión hará que el servicio no responda. Puede gestionar las conexiones desde la aplicación a través de la característica de agrupación de conexiones del controlador.

## Tiempos de espera del proxy

Los portales HAProxy gestionan el ciclo de vida de las conexiones entre el servidor y el cliente. Los detallamos aquí como una referencia para los escritores de controladores y otros que tienen interés en la actividad de bajo nivel de las conexiones de base de datos de {{site.data.keyword.composeForEtcd}}.

Valor | Valor | Se aplica
----------|-----------|-----------
cliente | 1 día | Cuando se espera que el cliente reconozca o envíe datos.
connect | 1m | Cuando se realiza una conexión entre el proxy y el servidor.
servidor | 1 día | Cuando se espera que el servidor reconozca o envíe datos.
check | 1m | Como una comprobación de tiempo de espera secundaria, cuando se realiza una conexión entre el proxy y el servidor.
{: caption="Tabla 1. Tiempos de espera de HAProxy etcd" caption-side="top"}
