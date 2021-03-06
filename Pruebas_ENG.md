## **Author**

| Company | Date | Version |
|:-:|:-:|:-:|
| <img src="/images/inspide2.png" alt="INSPIDE" width="100"/>  | 12/03/2019 | 2.0 |

## **Speaker**

| Image  |  Name |  Company |Position|email|Linkedin|
|:-:|:-:|:-:|:-:|:-:|:-:|
|  <img src="/images/jgcasta_bn.png" alt="INSPIDE" width="50"/> | José Gómez Castaño  | <img src="/images/inspide2.png" alt="INSPIDE" width="100"/>   | **CTO** | jgcasta@inspide.com 	| [linkedin.com/in/josegomezcastano](https://linkedin.com/in/josegomezcastano) |

## Support Contact

To solve any doubt or incident, a mailbox has been opened in which these: soporte@cmobility30.es

# **Index**

1. [Practice information](#id1)
	1. [Automatic generation of the client](#id1.1)
2. [Practical exercises](#id2)
	1. [Identification in the service](#id21)
	2. [Application for nested PMVs](#id22)
	3. [Request for PMVs in a Province](#id23)
	4. [Request of PMVs of a Type](#id24)
	5. [Application for PMVs of a highway](#id25)
	6. [Request PMVs of a highway between two kilometric points](#id26)
3. [National Access Point publication](#id3)

# Practical **information** <a name="id1"></a>

<img src="/images/question.png" alt="API" width="20"/> **API Documentation 'Bandeja de Salida'**


The API information of the API **'Bandeja de Salida'** can be found in the following URLs: [Apiary](https://bandejasalidaeng.docs.apiary.io) (Free access) and [Swagger](https://bandejadesalida-dev.cmobility30.es:8443/swagger-ui.html) (Certificate required).

The interface has been updated to allow the publication of LINCE and Works in progress incidents. Along with this information, the information obtained from the V16 signal has been published. The associated documentation can be found in the document [Bandeja de Salida specification 1.3](https://github.com/INSPIDE/DGT3.0Workshop1/blob/master/aux/20200124%20API%20Bandeja%20Salida%20v.1.3.pdf) The relationship between LINCE incidents and the iconography is described in [20191010_DGT30_0.xlsx](https://github.com/INSPIDE/DGT3.0Workshop1/blob/master/aux/20191010_DGT30_0.xlsx)

<img src="/images/question.png" alt="API" width="20"/> **Tools**


For the execution of the tests the use of a REST Client is necessary. The * download * of  [Postman](https://www.getpostman.com/downloads/) that is proposed as a client for the follow-up of the workshop.

<img src="/images/question.png" alt="API" width="20"/> **Sequence diagram**.

<img src="/images/diagramasecuencia.png">

## *1.1* Automatic generation of a client <a name="id1.1"></a>

Since the publication of the API is based on SWAGGER, it is possible to use the utility [swagger-codegen-cli](https://search.maven.org/classic/#search%7Cgav%7C1%7Cg%3A%22io.swagger%22%20AND%20a%3A%22swagger-codegen-cli%22) to generate a complete application, from the JSON file obtained from the download https://bandejadesalida-dev.cmobility30.es:8443/v2/api-docs (Certificate required).


## *00.* - Master tables <a name="id21"></a>

For filtering the information of the active PMVV at each moment, it is necessary to send a JSON with the filtering attributes, which responds to the following example

```json
{
  "idcompany": "INSPIDE",
  "token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
  "type": 0,
  "province": 28,
  "road": "A2",
  "kpfrom": 2,
  "kpto": 50,
  "direction": 3,
  "mode": 3,
  "category": 3,
  "withgeom": 1
}
```

The attributes are encoded and can be consulted by invoking the GET method of the corresponding master table. These are constantly updated in https://bandejadesalida-dev.cmobility30.es:8443/swagger-ui.html (Certificate required).

## Changes in the Master tables

Changes in any of the tables is notified by an MQTT message to the topic **out.changetables** according to the following sequence diagram.

<img src="images/secnotifmastertables.png" alt="Ayuda" />

```json
{
    "code": 1,
    "data": [],
    "desc": "MasterTables have a change"
}
```

In this case, or when desired, you can consult the last actaulilzación them to request their content, using the method **/api/1.0/mastertables/getChangeTables** , which returns the following message.

```json
{
  "errorCode": 0,
  "errorDesc": "OK",
  "data": [
    {
      "idchange": 1,
      "tschange": "2019-02-20T05:00:00.000+0000",
      "tablename": "Categories"
    },
    {
      "idchange": 2,
      "tschange": "2019-02-20T01:00:00.000+0000",
      "tablename": "ErrorCodes"
    }
	]
}
```


# Practical **exercises** <a name="id2"></a>

## *01.* - Identification in the service <a name="id21"></a>

Example **a | Correct identification**

To carry out the operations of the API it is necessary to obtain a session token that will expire in a random way throughout the same. The operation that allows obtaining it is **/api/1.0/getToken** that returns the following result:

<img src="images/diagramasecuencia.png" alt="Ayuda" />

```json
{
  "errorCode": 0,
  "errorDesc": "OK",
  "data": [
    {
      "token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f"
    }
  ]
}
```
The authentication process is based on digital client certificates. For the realization of tests and subsequent production, the client must complete the documentation provided in which they are requested the necessary data of the company that will consume the services. The certificate will be issued by the PKI of the platform and delivered physically to the person responsible for it.

> <img src="/images/explain.png" alt="Explanation" width="20"/>		**Explanation**
>
> It is a correct identification thanks to the introduction of the values `token`e`idcompany`. The token is temporarily provided by the service, and idcompany corresponds to the CN field of the client digital certificate.
>

Example **b | Correct request**

```json
{
    "category": 15,
    "idcompany": "cn.correcto",
    "token": "token.correcto",
    "withgeom": 1
}
```

If the identification is wrong, you get the following message

```json
{
    "errorCode": 10,
    "errorDesc": "Authorization error",
    "data": []
}
```

Example **c | Incorrect request by `idcompany`**


> <img src="/images/explain.png" alt="Explanation" width="20"/>		**Explanation**
>
> Valid `idcompany` is not provided.
>
> - Error Code: ** 10 **
> - Error description: ** Authorization error **
>

``` json
	{
	"idcompany": "cn.erroneo",
	"token": "token.correcto",
	"category": 15,
	"withgeom":1
	}
```

Example **d | Incorrect request by `token`**

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> Valid `token` is not provided.
>
> - Error Code: ** 10 **
> - Error description: ** Authorization error **
>

``` json
	{
	"idcompany": "cn.correcto",
	"token": "token.erroneo",
	"category": 15,
	"withgeom":1
	}
```

Example **e | Incorrect request by `token` and` idcompany`**

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> It is a bad identification because the `token` value has been entered incorrectly as well as the` idcompany` value.
>
> - Error Code: ** 10 **
> - Error description: ** Authorization error **
>

``` json
	{
	"idcompany": "cn.erroneo",
	"token": "token.erroneo",
	"category": 15,
	"withgeom":1
	}
```



## *02.* - Request for nested PMVs <a name="id22"> </a>

Example ** a | Correct request **

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> Correct application of the alphanumeric and geographic information (`withgeom`) of the set of Virtual Message Panels according to the following attributes: `type`,`province`,`road`, `kpfrom`,`kpto`,`direction`,`mode`,`category` that are indicated in the following Table:
>
> | Type | Province | Road | PK home | Final station | Address | Mode | Category | Geometries |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  **Point** |  **Madrid** | **A-2** |  **2** |	**40** |  **Both** |  **Motorcycle** | **Air quality**  | **Yes** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
	"type": 1,
	"province": 28,
	"road": "A-2",
	"kpfrom": 2,
	"kpto": 40,
	"direction":1,
	"mode": 3,
	"category": 15,
	"withgeom":1
	}
```

## *03.* - Request of PMVs in a Province <a name="id23"></a>

Example ** a | Correct request **

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> Correct application of the alphanumeric and geographic information (`withgeom`) of the set of Virtual Message Panels according to the following attributes: `province` that are indicated in the following Table:
>
> | Type | Province | Road | PK home | Final station | Address | Mode | Category | Geometries |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | na |  na |	na |  na |  na | na | **Yes** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
	"province": 28,
	"withgeom":1
	}
```

Example **b | Incorrect request by `province`**

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> It is an erroneous request because the `province` value has been entered incorrectly since it is not an *integer*.
>
> - Error Code: **3**
> - Descripción del error: **Province must be an integer value**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
	"province": "Texto",
	"withgeom":1
	}
```


## *04.* - Request PMVs of a highway between two kilometric points<a name="id26"></a>


Example **a | Correct request**

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> Correct application of the alphanumeric and geographic information (`withgeom`) of the set of Virtual Message Panels according to the following attributes: `province`,`road`,`kpfrom`,`kpto` that are indicated in the following Table:
>
> | Type | Province | Road | PK home | Final station | Address | Mode | Category | Geometries |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | **A-2** |  **2** | **40** |  na |  na | na | **Yes** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
	"province":28,
	"road": "A-2",
	"kpfrom": 2,
	"kpto": 40,
	"withgeom":1
	}
```

Example **b | Incorrect request for `kpfrom` less than `kpto`**

> <img src="/images/explain.png" alt="Explanation" width="20"/>	**Explanation**
>
> This is an erroneous request because the values have been inconsistently entered of the initial kilometric point and final kilometer point being `kpto`>` kpfrom`
>
> - Error Code: **5**
> - Error description: **Kp from must be lower than Kp to**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "28a9e96167a6ee0f84bb9c46e8a3b381032f7d9de59ce882539db044e4ee691f",
	"province":28,
	"road": "A-2",
	"kpfrom": 40,
	"kpto": 2,
	"withgeom":1
	}
```

# National Access Point information <a name="id3"></a>

Through the operation ** GET ** at the endpoint **/api/1.0/nap ** it is possible to obtain all the events that are published in the National Access Point of Spain that is under your responsibility DGT. The returned dataset follows the DATEXII standard

```xml
<?xml version="1.0" encoding="UTF-8"?>
<d2LogicalModel modelBaseVersion="1.0" xsi:schemaLocation="http://datex2.eu/schema/1_0/1_0 http://datex2.eu/schema/1_0/1_0/DATEXIISchema_1_0_1_0.xsd" xmlns="http://datex2.eu/schema/1_0/1_0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <exchange>
        <supplierIdentification>
            <country>es</country>
            <nationalIdentifier>dgt</nationalIdentifier>
        </supplierIdentification>
    </exchange>
    <payloadPublication xsi:type="_0:SituationPublication" lang="es" xmlns:_0="http://datex2.eu/schema/1_0/1_0">
	.....................
	.....................
    </payloadPublication>
</d2LogicalModel>
```
The data use guide is available in [DATEXII Use Guide](http://infocar.dgt.es/datex2/informacion_adicional/Guia%20de%20Utilizacion%20de%20DATEX%20II.pdf)

DATEXII libraries with extensions in Spain are available for download at [Librerias de parseo para DATEXII](http://infocar.dgt.es/datex2/informacion_adicional/Ayuda%20desarrollador/Librerias%20Java)

© 2018-2020 DGT. All rights reserved.
