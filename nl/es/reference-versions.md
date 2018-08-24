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

# Versiones
{: #versions}

Versiones desplegables | Versión preferida
----------|-----------
3.2.18. 3.3.3 | 3.2.18, 3.3.3
{: caption="Tabla 1. Versiones de {{site.data.keyword.composeForEtcd}}" caption-side="top"}

## Versión preferida

La versión preferida es normalmente la versión más reciente de la base de datos etcd que está disponible para {{site.data.keyword.composeForEtcd}}. Es la versión que es el valor predeterminado en el selector de versión desplegable de la página de catálogo. También es la versión que la API suministra automáticamente si no se especifica ninguna versión en la llamada.

### Nuevo protocolo de versión preferido

Cuando una nueva versión está disponible, su release se anuncia y la versión está disponible para el despliegue. Después del release, hay una ventana de 7 días aproximadamente en la que está disponible la versión más reciente, pero no aparece como la versión preferida. Esta ventana permite a los usuarios desplegar y probar la nueva versión, mientras aún tiene la versión actual disponible para ellos. También permite a los ingenieros de Compose detectar y arreglar cualquier problema que surja en la nueva versión. Al final de la ventana de 7 días, la nueva versión se establece como la versión preferida, o se anuncia una nueva fecha para este cambio.

La lista de versiones disponibles para los suministros se encuentra en la [página de catálogo](https://console.{DomainName}/catalog/services/compose-for-etcd) de {{site.data.keyword.composeForEtcd}}.

Para obtener una lista actual de las versiones disponibles para el servicio de {{site.data.keyword.composeForEtcd}}, puede utilizar el punto final
[GET /2016-07/deployments/:id/versions](https://apidocs.compose.com/v1.0/reference#2016-07-get-deployments-versions).
