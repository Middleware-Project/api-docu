---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introducción

La presente documentación hace referencia a la API del middleware IoT perteneciente al taller profesional. En primer lugar se presenta el procedimiento de autenticación de usuarios acorde a JSON-Web token. Luego se documenta la API genérica del proyecto y la API destinada a la integración con IGEO.

# Autenticación
## Authenticate

### Autenticar usuario 

```shell
curl -X POST \
  http://localhost:3000/api/v1/authenticate \
  -d '{"email":"example@mail.com","password":"123123123"}'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "auth_token": "eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1Mjg..."
}
```
Esta llamada permite autenticar usuarios en el sistema proporcionando email y password. Para realizar request en el sistema es necesario adjuntar en el Header de cada llamada de la siguiente forma: 

`Authorization: token....`

<aside class="notice">
Se debe reemplazar <code>token...</code> con el token personal entregado.
</aside>

#### HTTP Request

`POST http://localhos:3000/api/v2/authenticate`

#### Parametros Body

Parametro | Descripción
--------- | -----------
email | Email de usuario
password | Contraseña de usuaior


# API Base
## Groups

### Obtener todos los grupos

```shell
curl http://localhos:3000/api/v1/groups \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "id": 1,
            "name": "Sala de reuniones",
            "description": "Sala ubicada en el primer piso",
            "created_at": "2018-05-18T09:02:37.418Z",
            "updated_at": "2018-05-18T09:02:37.418Z"
        },
        {
            "id": 2,
            "name": "Sala de reuniones",
            "description": "Sala ubicada en el primer piso",
            "created_at": "2018-05-23T19:50:57.185Z",
            "updated_at": "2018-05-23T19:50:57.185Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todos los grupos

#### HTTP Request

`GET http://localhos:3000/api/v1/groups`


### Obtener un grupo en especifico

```shell
curl http://localhos:3000/api/v1/groups/1 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": {
        "group": {
            "id": 1,
            "name": "Sala de reuniones",
            "description": "Sala ubicada en el primer piso",
            "created_at": "2018-05-18T09:02:37.418Z",
            "updated_at": "2018-05-18T09:02:37.418Z"
        },
        "nodes": [
            {
                "id": 1,
                "modelName": "pysense",
                "manufacterName": "pycom",
                "description": "sensor",
                "group_id": 1,
                "created_at": "2018-05-18T09:02:40.195Z",
                "updated_at": "2018-05-18T09:02:40.195Z"
            },
            {
                "id": 2,
                "modelName": "pysense",
                "manufacterName": "pycom",
                "description": "sensor",
                "group_id": 1,
                "created_at": "2018-05-18T09:03:29.664Z",
                "updated_at": "2018-05-18T09:03:29.664Z"
            }
        ]
    }
}
```

Esta llamada retorna la información especifica de un groupo. Además muestra todos los nodos asociados a este.

#### HTTP Request

`GET http://localhos:3000/api/v1/groups/<ID>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del grupo a retornar

### Crear un grupo

```shell
curl -X POST \
  http://localhost:3000/api/v1/groups \
  -H "Authorization: token..." \
  -d '{
	"name": "Sala de reuniones",
	"description": "Sala ubicada en el primer piso"
}'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 201,
        "message": "Grupo creado"
    },
    "data": {
        "id": 2,
        "name": "Sala de reuniones",
        "description": "Sala ubicada en el primer piso",
        "created_at": "2018-05-23T19:50:57.185Z",
        "updated_at": "2018-05-23T19:50:57.185Z"
    }
}
```

Este request permite crear un grupo en especifico.

#### HTTP Request

`POST http://localhost:3000/api/v1/groups`

#### Parametros URL

Parametros | Descripción
--------- | -----------
name | nombre del grupo
description | descripción del grupo

## Nodes

### Obtener todos los nodos

```shell
curl GET \
  http://localhost:3000/api/v1/nodes \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "id": 1,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:02:40.195Z",
            "updated_at": "2018-05-18T09:02:40.195Z"
        },
        {
            "id": 2,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:03:29.664Z",
            "updated_at": "2018-05-18T09:03:29.664Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todos los nodos pertenecientes al sistema.

#### HTTP Request

`GET http://localhos:3000/api/v1/nodes`

### Obtener un nodo en especifico

```shell
curl http://localhos:3000/api/v1/nodes/5 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": {
        "node": {
            "id": 5,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:21:54.471Z",
            "updated_at": "2018-05-18T09:21:54.471Z"
        },
        "sensors": [
            {
                "id": 1,
                "name": "temperature",
                "description": "sensor que permite medir temperatura",
                "units": "Cº",
                "created_at": "2018-05-18T09:17:39.624Z",
                "updated_at": "2018-05-18T09:17:39.624Z"
            },
            {
                "id": 2,
                "name": "humidity",
                "description": "sensor de humedad",
                "units": "%",
                "created_at": "2018-05-18T09:18:08.022Z",
                "updated_at": "2018-05-18T09:18:08.022Z"
            }
        ]
    }
}
```
Esta llamada retorna la infromación de un nodo en especifico. Además se adjunta un listado de sensores que soporta.

#### HTTP Request

`GET http://localhos:3000/api/v1/nodes/<ID>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del nodo a retornar

### Crear un Nodo

```shell
curl -X POST \
  http://localhost:3000/api/v1/nodes \
  -H "Authorization: token..." \
  -d '{
	"modelName": "pysense",
	"manufacterName": "pycom",
	"description": "sensor",
	"group_id": 1,
	"sensors":[{"name":"temperature"},{"name":"humidity"}]
	
    }'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 201,
        "message": "Nodo creado"
    },
    "data": {
        "id": 1,
        "modelName": "pysense",
        "manufacterName": "pycom",
        "description": "sensor",
        "group_id": 1,
        "created_at": "2018-05-24T06:17:13.257Z",
        "updated_at": "2018-05-24T06:17:13.257Z"
    }
}
```

Esta llamada permite crear un nodo asociado a un grupo y sensores especificos.

#### HTTP Request

`POST http://localhos:3000/api/v1/nodes`

#### Parametros URL

Parametro | Descripción
--------- | -----------
modelName | modelo del nodo
manufacterName | nombre del desarrollador
description | descripción del nodo
group_id | ID del grupo al cual pertenece
sensors | arreglo de nodos asociados

-------------------------------------------------
## Sensors

### Obtener todos los sensores

```shell
curl GET \
  http://localhost:3000/api/v1/sensors \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
          "id": 1,
          "name": "temperature",
          "description": "sensor que permite medir temperatura",
          "units": "Cº",
          "created_at": "2018-05-18T09:17:39.624Z",
          "updated_at": "2018-05-18T09:17:39.624Z"
        },
        {
          "id": 2,
          "name": "humidity",
          "description": "sensor de humedad",
          "units": "%",
          "created_at": "2018-05-18T09:18:08.022Z",
          "updated_at": "2018-05-18T09:18:08.022Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todos los sensores pertenecientes al sistema.

#### HTTP Request

`GET http://localhos:3000/api/v1/sensors`

### Obtener un sensor en especifico

```shell
curl http://localhos:3000/api/v1/sensors/1 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": {
        "sensor": {
            "id": 1,
            "name": "temperature",
            "description": "sensor que permite medir temperatura",
            "units": "Cº",
            "created_at": "2018-05-18T09:17:39.624Z",
            "updated_at": "2018-05-18T09:17:39.624Z"
        }
    }
}
```
Esta llamada retorna la infromación de un sensor en especifico.

#### HTTP Request

`GET http://localhos:3000/api/v1/sensors/<ID>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del sensor a retornar

### Crear un sensor

```shell
curl -X POST \
  http://localhost:3000/api/v1/sensors \
  -H "Authorization: token..."
  -d '{
	"name": "humidity",
	"description": "sensor de humedad",
	"units": "%"
    }'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 201,
        "message": "Sensor creado"
    },
    "data": {
        "id": 5,
        "name": "humidity",
        "description": "sensor de humedad",
        "units": "%",
        "created_at": "2018-05-24T06:13:39.780Z",
        "updated_at": "2018-05-24T06:13:39.780Z"
    }
}
```

Esta llamada permite crear un sensor especifico.

#### HTTP Request

`POST http://localhos:3000/api/v1/sensors`

#### Parametros URL

Parametro | Descripción
--------- | -----------
name | nombre del sensor
description | descripción del sensor
unit| unidad de medida sensor

## Measures

### Obtener todas las mediciones

```shell
curl GET \
  http://localhost:3000/api/v1/measures \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "id": 1,
            "data": 24.4,
            "unit": "Cº",
            "node_id": 5,
            "sensor_id": 1,
            "created_at": "2018-05-18T09:52:32.342Z",
            "updated_at": "2018-05-18T09:52:32.342Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todas las mediciones pertenecientes al sistema.

#### HTTP Request

`GET http://localhos:3000/api/v1/measures`

### Obtener una medición en especifica

```shell
curl http://localhos:3000/api/v1/measures/1 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": {
        "measure": {
            "id": 1,
            "data": 24.4,
            "unit": "Cº",
            "node_id": 5,
            "sensor_id": 1,
            "created_at": "2018-05-18T09:52:32.342Z",
            "updated_at": "2018-05-18T09:52:32.342Z"
        },
        "node": {
            "id": 5,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:21:54.471Z",
            "updated_at": "2018-05-18T09:21:54.471Z"
        },
        "sensor": {
            "id": 1,
            "name": "temperature",
            "description": "sensor que permite medir temperatura",
            "units": "Cº",
            "created_at": "2018-05-18T09:17:39.624Z",
            "updated_at": "2018-05-18T09:17:39.624Z"
        }
    }
}
```
Esta llamada retorna la infromación de un sensor en especifico.

#### HTTP Request

`GET http://localhos:3000/api/v1/measures/<ID>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID de la medición a retornar

# API IGEO

## Nodes

### Obtener todos los nodos

```shell
curl GET \
  http://198.199.68.64/api/v2/nodes \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "id": 1,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:02:40.195Z",
            "updated_at": "2018-05-18T09:02:40.195Z"
        },
        {
            "id": 2,
            "modelName": "pysense",
            "manufacterName": "pycom",
            "description": "sensor",
            "group_id": 1,
            "created_at": "2018-05-18T09:03:29.664Z",
            "updated_at": "2018-05-18T09:03:29.664Z"
        }
    ]
}
```

Permite obtener el listado de todos los nodos pertenecientes al sistema.

#### HTTP Request

`GET http://198.199.68.64/api/v2/nodes`

### Obtener un nodo en especifico

```shell
curl http://198.199.68.64/api/v2/nodes/01001 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "node": {
                "id": 5,
                "modelName": "pysense",
                "manufacterName": "pycom",
                "description": "device",
                "status":true,
                "group_id": 1,
                "created_at": "2018-05-18T09:21:54.471Z",
                "updated_at": "2018-05-18T09:21:54.471Z"
            },
            "sensors": [
                {
                    "id": 1,
                    "name": "temperature",
                    "description": "sensor que permite medir temperatura",
                    "units": "Cº",
                    "created_at": "2018-05-18T09:17:39.624Z",
                    "updated_at": "2018-05-18T09:17:39.624Z"
                },
                {
                    "id": 2,
                    "name": "humidity",
                    "description": "sensor de humedad",
                    "units": "%",
                    "created_at": "2018-05-18T09:18:08.022Z",
                    "updated_at": "2018-05-18T09:18:08.022Z"
                }
            ]
        }
    ]
}
```
Permite obtener el listado de nodos pertenecientes a un grupo. Además se adjunta la información de los sensores asociados a estos.

#### HTTP Request

`GET http://198.199.68.64/api/v2/nodes/<group_id>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
group_id | ID del grupo en particular (Obligatorio)

### Crear un Nodo

```shell
curl -X POST \
  http://198.199.68.64/api/v2/nodes \
    -H "Authorization: token..."
  -d '{
	"modelName": "pysense",
	"manufacterName": "pycom",
	"description": "sensor",
	"group_id": 1001,
	"sensors":[{"id":1},{"id":2}]
	
}'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 201,
        "message": "Nodo creado"
    },
    "data": {
        "id": 1,
        "modelName": "pysense",
        "manufacterName": "pycom",
        "description": "sensor",
        "status":false,
        "group_id": 01001,
        "created_at": "2018-05-24T06:17:13.257Z",
        "updated_at": "2018-05-24T06:17:13.257Z"
    }
}
```

Esta llamada permite crear un nodo asociado a un grupo y sensores especificos.

#### HTTP Request

`POST http://198.199.68.64/api/v2/nodes`

#### Parametros URL

Parametro | Descripción
--------- | -----------
modelName | modelo del nodo *
manufacterName | nombre del desarrollador *
description | descripción del nodo
group_id | ID del grupo al cual pertenece *
sensors | arreglo de ids sensores asociados *

*Campo obligatorio

-------------------------------------------------
## Sensors

### Obtener todos los sensores

```shell
curl GET \
  http://198.199.68.64/api/v2/sensors \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
          "id": 1,
          "name": "temperature",
          "description": "sensor que permite medir temperatura",
          "units": "Cº",
          "created_at": "2018-05-18T09:17:39.624Z",
          "updated_at": "2018-05-18T09:17:39.624Z"
        },
        {
          "id": 2,
          "name": "humidity",
          "description": "sensor de humedad",
          "units": "%",
          "created_at": "2018-05-18T09:18:08.022Z",
          "updated_at": "2018-05-18T09:18:08.022Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todos los sensores pertenecientes al sistema.

#### HTTP Request

`GET http://198.199.68.64/api/v2/sensors`

### Obtener un sensor en especifico

```shell
curl http://198.199.68.64/api/v2/sensors/1 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": {
        "sensor": {
            "id": 1,
            "name": "temperature",
            "description": "sensor que permite medir temperatura",
            "units": "Cº",
            "created_at": "2018-05-18T09:17:39.624Z",
            "updated_at": "2018-05-18T09:17:39.624Z"
        }
    }
}
```
Esta llamada retorna la infromación de un sensor en especifico.

#### HTTP Request

`GET http://198.199.68.64/api/v2/sensors/<ID>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del sensor a retornar

### Crear un sensor

```shell
curl -X POST \
  http://198.199.68.64/api/v2/sensors \
    -H "Authorization: token..."
  -d '{
	"name": "humidity",
	"description": "sensor de humedad",
	"units": "%"
}'
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 201,
        "message": "Sensor creado"
    },
    "data": {
        "id": 5,
        "name": "humidity",
        "description": "sensor de humedad",
        "units": "%",
        "created_at": "2018-05-24T06:13:39.780Z",
        "updated_at": "2018-05-24T06:13:39.780Z"
    }
}
```

Esta llamada permite crear un sensor especifico.

#### HTTP Request

`POST http://198.199.68.64/api/v2/sensors`

#### Parametros URL

Parametro | Descripción
--------- | -----------
name | nombre del sensor
description | descripción del sensor
unit| unidad de medida sensor

## Measures

### Obtener todas las mediciones

```shell
curl GET \
  http://198.199.68.64/api/v2/measures?node_id=1&sensor_id=2&limit=10 \
    -H "Authorization: token..."
```

> El comando anterior retorna un JSON con la siguiente estructura

```json
{
    "succes": {
        "status": 200
    },
    "data": [
        {
            "id": 1,
            "data": 24.4,
            "unit": "Cº",
            "node_id": 5,
            "sensor_id": 1,
            "created_at": "2018-05-18T09:52:32.342Z",
            "updated_at": "2018-05-18T09:52:32.342Z"
        }
    ]
}
```

Esta llamada permite obtener el listado de todas las mediciones pertenecientes a un grupo determinado.

#### HTTP Request

`GET http://198.199.68.64/api/v2/measures?node_id=<node_id>&sensor_id=<sensor_id>&limit=<limit>`

#### Parametros URL

Parametro | Descripción
--------- | -----------
node_id | ID node *
sensor_id | ID sensor *
limit | Cantidad requerida

*Campo obligatorio
