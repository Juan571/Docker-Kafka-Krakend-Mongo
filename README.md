# Configuración de Docker, para mongo, kafka y krakend en un entorno local.

Se hace uso de docker compose para establecer un entorno local, que hace uso de mongo con persistencia para el almacenamiento de datos,
de kafka con zookeeper para el manejo de colas de mensajes, y de krakend como gateway

## Comenzando 🚀




### Requisitos 📋

_Que cosas necesitas para instalar_


* [Docker: ](https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe) - https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe

* [Robot 3t: ](https://robomongo.org/download) - https://robomongo.org/download

* [Kafka Tool: ](https://www.kafkatool.com/download2/kafkatool_64bit.exe) - https://robomongo.org/download


### Instalación 🔧

_Una vez descargadas todas las herramientas anteriores, se procede a ejecutar el docker compose con la configuracion que existe en docker-compose.yml_

_Para eso, ejecutamos el siguiente comando en la raiz de la carpeta Docker: _

```
docker-compose up --build -d
```
Aclarando los siguientes parametros:

* --build -> para construir los containers
* -d -> detach , para soltar la consola una vez constuido el stack


## Verificamos los containers ejecutandose ⚙️

_Ejecutamos lo siguiente_
```
docker ps
```
_Deberia de mostrarnos algo similar a esto:_


| CONTAINER ID  | IMAGE | COMMAND | CREATED | STATUS | PORTS | NAMES |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 6158dba7cb89 | docker_krakend | "/usr/bin/krakend ru…" | 45 hours ago | Up 45 hours | 8000/tcp, 8090/tcp, 0.0.0.0:8080->8080/tcp | krakend_dev |
| ccf5415b3895 | docker_kafka-server | "/opt/bitnami/script…" | 6 weeks ago | Up 5 days | 0.0.0.0:9092->9092/tcp | kafka_cluster_dev |
|0b333edd84b4| docker_mongo |"docker-entrypoint.s…" |6 weeks ago | Up 5 days | 0.0.0.0:27017->27017/tcp   |mongo_dev|
|6297e4af31f2| bitnami/zookeeper:latest |"/opt/bitnami/script…"|6 weeks ago|Up 5 days| 2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp, 8080/tcp | zookeeper_dev|

_mostrando cada uno de los servicios descritos en docker-compose.yml_




Comandos para levantar el consumer o el producer en el mismo container de Kafka

/opt/bitnami/kafka/bin/kafka-console-consumer.sh  --bootstrap-server localhost:9092 --topic third-party --from-beginning

/opt/bitnami/kafka/bin/kafka-console-producer.sh  --bootstrap-server localhost:9092 --topic third-party