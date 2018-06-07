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

La presente documentación hace referencia a la API del middleware IoT perteneciente al taller profesional.

# Groups

## Obtener todos los grupos

```shell
curl "http://localhos:3000/api/v1/groups"
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

### HTTP Request

`GET http://localhos:3000/api/v1/groups`


## Obtener un grupo en especifico

```shell
curl "http://localhos:3000/api/v1/groups/1"
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

### HTTP Request

`GET http://localhos:3000/api/v1/groups/<ID>`

### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del grupo a retornar

## Crear un grupo

```shell
curl -X POST \
  http://localhost:3000/api/v1/groups \
  -H 'Content-Type: application/json' \
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

### HTTP Request

`POST http://localhost:3000/api/v1/groups`

### Parametros URL

Parametros | Descripción
--------- | -----------
name | nombre del grupo
description | descripción del grupo

# Nodes

## Obtener todos los nodos

```shell
curl GET \
  http://localhost:3000/api/v1/nodes
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

### HTTP Request

`GET http://localhos:3000/api/v1/nodes`

## Obtener un nodo en especifico

```shell
curl "http://localhos:3000/api/v1/nodes/5"
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

### HTTP Request

`GET http://localhos:3000/api/v1/nodes/<ID>`

### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del nodo a retornar

## Crear un Nodo

```shell
curl -X POST \
  http://localhost:3000/api/v1/nodes \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: e32ec4f9-7286-43cd-96e0-86917df80054' \
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

### HTTP Request

`POST http://localhos:3000/api/v1/nodes`

### Parametros URL

Parametro | Descripción
--------- | -----------
modelName | modelo del nodo
manufacterName | nombre del desarrollador
description | descripción del nodo
group_id | ID del grupo al cual pertenece
sensors | arreglo de nodos asociados

-------------------------------------------------
# Sensors

## Obtener todos los sensores

```shell
curl GET \
  http://localhost:3000/api/v1/sensors
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

### HTTP Request

`GET http://localhos:3000/api/v1/sensors`

## Obtener un sensor en especifico

```shell
curl "http://localhos:3000/api/v1/sensors/1"
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

### HTTP Request

`GET http://localhos:3000/api/v1/sensors/<ID>`

### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID del sensor a retornar

## Crear un sensor

```shell
curl -X POST \
  http://localhost:3000/api/v1/sensors \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 2d106a27-37de-4a08-a133-b67fee68f145' \
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

### HTTP Request

`POST http://localhos:3000/api/v1/sensors`

### Parametros URL

Parametro | Descripción
--------- | -----------
name | nombre del sensor
description | descripción del sensor
unit| unidad de medida sensor

# Measures

## Obtener todas las mediciones

```shell
curl GET \
  http://localhost:3000/api/v1/measures
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

### HTTP Request

`GET http://localhos:3000/api/v1/measures`

## Obtener una medición en especifica

```shell
curl "http://localhos:3000/api/v1/measures/1"
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

### HTTP Request

`GET http://localhos:3000/api/v1/measures/<ID>`

### Parametros URL

Parametro | Descripción
--------- | -----------
ID | ID de la medición a retornar