---

copyright:
  years: 2016,2018
lastupdated: "2017-09-21"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de una aplicación {{site.data.keyword.cloud_notm}}

Para conectar una aplicación {{site.data.keyword.cloud}} al servicio, utilice las credenciales de servicio que se crean cuando se suministra el servicio. La app de ejemplo muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForEtcd}} utilizando las credenciales y cómo crear una base de datos y leer y escribir en la base de datos.

## Conexión mediante la app de ejemplo 'Hello World'

La app de ejemplo [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForEtcd}} utilizando las credenciales proporcionada. La aplicación crea, lee y escribe en una base de datos.

Descargue la app de ejemplo y siga las instrucciones del archivo readme. A continuación, en la página de detalles de la aplicación de {{site.data.keyword.cloud}}, pulse **Ver APP** para ver el contenido de la tabla *ejemplos*.

## Credenciales disponibles
{: #available-credentials}

Para conectar una app al servicio, utilice las credenciales creadas junto con el servicio. La app de ejemplo [compose-etcd-helloworld-nodejs](https://github.com/IBM-Cloud/compose-etcd-helloworld-nodejs) muestra cómo utilizar Node.js para conectar a un servicio de {{site.data.keyword.composeForEtcd}} utilizando las credenciales.

|Nombre de campo|Descripción|
|----------|-----------|
|`ca_certificate_base64` `(opcional)`|Un certificado codificado en base64 y firmado automáticamente que se utiliza para confirmar que una aplicación se está conectando al servidor apropiado. El certificado solo está presente en los servicios que tienen una firma autofirmada en lugar de un certificado Let's Encrypt. Debe decodificar la clave antes de poder utilizarla, como se muestra en la aplicación de ejemplo.|
|`deployment_id`|Un identificador interno para el servicio, tal como se ha creado en Compose.|
|`db_type`|El tipo de base de datos que ofrece el servicio; en este caso, `etcd`.|
|`name`|El nombre del despliegue de la base de datos.|
|`uri`|El URI que se utilizará al conectarse al servicio. `uri` incluye el esquema (`amqps:), el nombre de usuario y la contraseña del administrador, el nombre de host del servidor, el número de puerto al que se conecta y el nombre de `vhost.|
|`uri_direct_1`|Un URI secundario que se puede utilizar al conectarse al servicio. Formateado en cuanto a `uri`.|
{: caption="Tabla 1. Credenciales de Compose for etcd" caption-side="top"}

**Nota:** Dos portales `haproxy` proporcionan acceso al servicio etcd. Tanto `uri` como `uri_direct_1` pueden utilizarse para conectarse. En las aplicaciones, conmute entre `uri` y `uri_direct_1` para gestionar respuestas a fallos de conexión.
