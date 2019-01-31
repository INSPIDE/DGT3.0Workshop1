
# **Ponentes**

|Imagen|  Nombre | Empresa | Cargo | email  | Linkedin |
|:-|:-:|:-:|:-:|
| <img src="/images/jgcasta.png" alt="INSPIDE" width="50"/> |    José Gómez Castaño	| <img src="/images/inspide2.png" alt="INSPIDE" width="100"/> |  **CTO** | jgcasta@inspide.com 	| [linkedin.com/in/josegomezcastano](https://linkedin.com/in/josegomezcastano) | 
||   |  |  |   |  |
||   |  |  |   |  |

# **Índice**

1. [Información de práctica](#id1)
2. [Ejercicios prácticos](#id2)
	1. [Identificación en el servicio](#id21)
	2. [Solicitud de PMVs anidados](#id22)
	3. [Solicitud de PMVs en una Provincia](#id23)
	4. [Solicitud de PMVs de un Tipo](#id24)
	5. [Solicitud de PMVs de una carretera](#id25)
	6. [Solicitud de PMVs de una carretera entre dos puntos kilométricos](#id26)
	7. [Solicitud de PMVs en función del sentido de circulación](#id27)
	8. [Solicitud de PMVs en función del modo de transporte](#id28)
	9. [Solicitud de PMVs en función de la categoría del evento](#id29)
	10. [Solicitud de PMVs sin geometría, sólo valores alfanuméricos](#id210)

# Información **práctica** <a name="id1"></a>

> <img src="/images/question.png" alt="Ayuda" width="20"/> **Ayuda**
>
> Todos los ejercicios se realizarán utilizando el método
> **_getPmv_** que se encuentra disponible a través de *Postman*.
> La operativa normal para la utilización de los diferentes ejemplos
> consiste en *cortar + pegar* el código incluído en el ejemplo en el área _Body_ dentro del entorno de Postman.
>
>
> <img src="/images/question.png" alt="API" width="20"/> **Información API BS**
>
> La información al API de la **Bandeja de Salida** se encuentra en la siguiente url: [API BS](https://bandejasalida.docs.apiary.io/#reference/0/getroads/getcategories).
>
>

# Ejercicios **prácticos** <a name="id2"></a>


## *01.* - Identificación en el servicio <a name="id21"></a>

Ejemplo **a | Identificación correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>		**Explicación**
>
> Se trata de una identificación correcta gracias a la introducción de los valores `token`e`idcompany`.
>

``` json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"category": 15,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud incorrecta por `idcompany`**


> <img src="/images/explain.png" alt="Explicación" width="20"/>		**Explicación**
>
> Se trata de una identificación errónea debido a que se ha introducido el valor `idcompany` incorrectamente.
>
> - Código de Error: **10**
> - Descripción del error: **Authorization error**
>

``` json
	{
	"idcompany": "Texto",
	"token": "INSPIDEmola",
	"category": 15,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud incorrecta por `token`**

> <img src="/images/explain.png" alt="Explicación" width="20"/>	**Explicación**
>
> Se trata de una identificación errónea debido a que se ha introducido el valor `token` incorrectamente.
>
> - Código de Error: **10**
> - Descripción del error: **Authorization error**
>

``` json
	{
	"idcompany": "INSPIDE",
	"token": "Texto",
	"category": 15,
	"withgeom":1
	}
```

Ejemplo **d | Solicitud incorrecta por `token` e `idcompany`**

> <img src="/images/explain.png" alt="Explicación" width="20"/>	**Explicación**
>
> Se trata de una identificación errónea debido a que se ha introducido el valor `token` así como el valor `idcompany` incorrectamente.
>
> - Código de Error: **10**
> - Descripción del error: **Authorization error**
>

``` json
	{
	"idcompany": "Texto",
	"token": "Texto",
	"category": 15,
	"withgeom":1
	}
```



## *02.* - Solicitud de PMVs anidados <a name="id22"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `type`,`province`,`road`, `kpfrom`,`kpto`,`direction`,`mode`,`category` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  **Punto** |  **Madrid** | **A-2** |  **2** |	**40** |  **Ambos** |  **Ciclomotor / Motocicleta** | **Calidad del aire**  | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
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

## *03.* - Solicitud de PMVs en una Provincia <a name="id23"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `province` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | na |  na |	na |  na |  na | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province": 28,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud incorrecta por `province`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido el valor `province` incorrectamente ya que no es un valor *integer*.
>
> - Código de Error: **3**
> - Descripción del error: **Province must be an integer value**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province": "Texto",
	"withgeom":1
	}
```

## *04.* - Solicitud de PMVs de un Tipo <a name="id24"></a>


Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `type` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  **Punto** |  na | na |  na |	na |  na |  na | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"type": 1,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud incorrecta por `type`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido el valor `type` incorrectamente ya que no es un valor *válido*.
>
> - Código de Error: **9**
> - Descripción del error: **Type is not valid**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"type": 1000,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud incorrecta por `type`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido el valor `type` incorrectamente ya que no es un valor *integer*.
>
> - Código de Error: **9**
> - Descripción del error: **Type must be an integer value**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"type": "Texto",
	"withgeom":1
	}
```

## *05.* - Solicitud de PMVs de una carretera <a name="id25"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `province` y `road` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | A-2 |  na |	na |  na |  na | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province": 28,
	"road": "A-2",
	"withgeom":1
	}
```

Ejemplo **b | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `province` y `road` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | **A-2** |  na |	na |  na |  na | na | **Sí** |
>
>
> **Nota**
>
> El valor ‘0’ en el atributo “pmvProv” indica que se trata de PMV tipo área que intersecta con la Provincia solicitada (en este caso 28).
> Es debido a la información asociada a un PMV tipo área, no contienen la Provincia.
>


```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province": 28,
	"road": 10000,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `province` y `road` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | **A-2** |  na |	na |  na |  na | na | **Sí** |
>
>
> **Nota**
>
> El valor ‘0’ en el atributo “pmvProv” indica que se trata de PMV tipo área que intersecta con la Provincia solicitada (en este caso 28).
> Es debido a la información asociada a un PMV tipo área, no contienen la Provincia.
>

```json

	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province": 28,
	"road": "Texto",
	"withgeom":1
	}
```

## *06.* - Solicitud de PMVs de una carretera entre dos puntos kilométricos <a name="id26"></a>


Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `province`,`road`,`kpfrom`,`kpto` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  **Madrid** | **A-2** |  **2** | **40** |  na |  na | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province":28,
	"road": "A-2",
	"kpfrom": 2,
	"kpto": 40,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud incorrecta por `kpfrom` menor a `kpto`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido de forma incoherente los valores
> del Punto kilométrico inicial y Punto kilométrico final siendo `kpto`  > `kpfrom`
>
> - Código de Error: **5**
> - Descripción del error: **Kp from must be lower than Kp to**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"province":28,
	"road": "A-2",
	"kpfrom": 40,
	"kpto": 2,
	"withgeom":1
	}
```


## *07.* - Solicitud de PMVs en función del sentido de circulación <a name="id27"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `direction` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  **Ambos** |  na | na | **Sí** |
>


```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"direction":1,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `direction` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  **Ambos** |  na | na | **Sí** |
>
>
> **Nota**
>
> No existe el valor de direction 1000, luego no existen PMVs que coincidan con los criterios de búsqueda.
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"direction": 10000,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud incorrecta por `direction`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido el valor `direction` incorrectamente ya que no es un valor *integer*.
>
> - Código de Error: **7**
> - Descripción del error: **Direction must be an integer value**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"direction": "Texto",
	"withgeom":1
	}
```


## *08.* - Solicitud de PMVs en función del modo de transporte <a name="id28"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `mode` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  **Bicicleta** | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"mode": 3,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `mode` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  **Bicicleta** | na | **Sí** |
>
>
> **Nota**
>
> No existe el valor de mode 1000, luego no existen PMVs que coincidan con los criterios de búsqueda.
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"mode": 1000,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `mode` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  **Bicicleta** | na | **Sí** |
>
>
> **Nota**
>
> La consulta es válida en todos los campos, luego si existen PMVs que coincidan con los criterios de búsqueda, aparecerán dentro del array data.
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"mode": “10”,
	"withgeom":1
	}
```


## *09.* - Solicitud de PMVs en función de la categoría del evento <a name="id29"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `category` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  na | **Calidad del aire** | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"category": 15,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `category` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  na | **Calidad del aire** | **Sí** |
>
>
> **Nota**
>
> La consulta es válida en todos los campos, luego si existen PMVs que coincidan con los criterios de búsqueda, aparecerán dentro del array data.
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"category": 1000,
	"withgeom":1
	}
```

Ejemplo **c | Solicitud incorrecta por `category`**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Se trata de una solicitud errónea debido a que se ha introducido el valor `category` incorrectamente ya que no es un valor *integer*.
>
> - Código de Error: **11**
> - Descripción del error: **Category must be an integer value**
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"category": "Texto",
	"withgeom":1
	}
```

Ejemplo **d | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `category` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  na |  na | **Calidad del aire** | **Sí** |
>
>
> **Nota**
>
> La consulta es válida en todos los campos, luego si existen PMVs que coincidan con los criterios de búsqueda, aparecerán dentro del array data.
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"category": “15,1”,
	"withgeom":1
	}
```

## *10.* - Solicitud de PMVs sin geometría, sólo valores alfanuméricos <a name="id210"></a>

Ejemplo **a | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información alfanumérica y geográfica (`withgeom`) del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `direction` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  **Ambos** |  na | na | **Sí** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"direction":1,
	"withgeom":1
	}
```

Ejemplo **b | Solicitud correcta**

> <img src="/images/explain.png" alt="Ayuda" width="20"/>	**Explicación**
>
> Solicitud correcta de la información únicamente alfanumérica del conjunto de Paneles de Mensaje Virtual según los
> siguientes atributos: `direction` que se indican en la siguiente Tabla:
>
> |  Tipo |  Provincia  | Carretera  | PK inicio  | PK final | Dirección | Modo | Categoría | Geometrías |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> |  na |  na | na |  na |	na |  **Ambos** |  na | na | **No** |
>

```json
	{
	"idcompany": "INSPIDE",
	"token": "INSPIDEmola",
	"direction":1,
	"withgeom":0
	}
```

# **Autoría**

|Autor| Versión  |
|:-:|:-:|:-:|:-:|
|<img src="/images/inspide2.png" alt="Ayuda" width="100"/> 	|  0.**2** 	|
