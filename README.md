
# Projet_TER - Etude d'une pipeline de donnée

Ce projet utilise docker compose pour configurer et exécuter plusieurs services: Neo4j, Zeppelin, Zookeeper et Kafka.

### Prérequis

Pour exécuter ce conteneur, vous devez avoir Docker installé.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)

### Utilisation

#### Démarrer les services

Pour démarrer tous les services définis dans le fichier `docker-compose.yml`, exécutez :

```shell
docker-compose up
```

Cela démarrera les services suivants :
- **Neo4j** : Une base de données de graphes.
- **Zeppelin** : Notebook web qui permet des analyses de données interactives.
- **Zookeeper** : Un service centralisé pour maintenir des informations de configuration, de nommage, fournir une synchronisation distribuée et des services de groupe.
- **Kafka** : Une plateforme de streaming d'événements distribués.

#### Arrêter les services

Pour arrêter les services, utilisez :

```shell
docker-compose down
```

#### Paramètres du conteneur

Pour exécuter un service spécifique, vous pouvez utiliser la commande suivante :

```shell
docker-compose run <nom_du_service>
```

Par exemple, pour exécuter Neo4j :

```shell
docker-compose run neo4j
```

Pour ouvrir un shell bash dans le conteneur Zeppelin :

```shell
docker-compose run zeppelin bash
```

#### Variables d'environnement

Chaque service a des variables d'environnement spécifiques configurées dans le fichier `docker-compose.yml` :

- **Neo4j** :
  - `NEO4J_AUTH` : Identifiants d'authentification (par défaut : neo4j/zeppelin)
  - `NEO4J_dbms_memory_heap_max__size` : Taille maximale du tas (par défaut : 8G)
  - `NEO4J_dbms_security_procedures_unrestricted` : Procédures non restreintes (par défaut : apoc.*)
  - `NEO4J_kafka_zookeeper_connect` : Chaîne de connexion Zookeeper
  - `NEO4J_kafka_bootstrap_servers` : Serveurs bootstrap Kafka
  - `NEO4J_dbms_logs_debug_level` : Niveau de débogage des journaux (par défaut : DEBUG)

- **Zookeeper** :
  - `ZOOKEEPER_CLIENT_PORT` : Port client (par défaut : 2181)
  - `ZOOKEEPER_TICK_TIME` : Temps de tick (par défaut : 2000)

- **Kafka** :
  - `KAFKA_ADVERTISED_LISTENERS`
  - `KAFKA_LISTENER_SECURITY_PROTOCOL_MAP`
  - `KAFKA_LISTENERS`
  - `CONFLUENT_METRICS_REPORTER_BOOTSTRAP_SERVERS`
  - `KAFKA_INTER_BROKER_LISTENER_NAME`
  - `KAFKA_BROKER_ID`
  - `KAFKA_ZOOKEEPER_CONNECT`
  - `KAFKA_METRIC_REPORTERS`
  - `KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR`
  - `KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS`
  - `CONFLUENT_METRICS_REPORTER_ZOOKEEPER_CONNECT`

#### Volumes

Chaque service a des mappages de volumes spécifiques :

- **Neo4j** :
  - `./neo4j/plugins:/plugins`
  - `./neo4j/data:/data`
  - `./neo4j/logs:/logs`

- **Zeppelin** :
  - `./zeppelin/notebook:/zeppelin/notebook`
  - `./zeppelin/conf:/zeppelin/conf`
  - `./zeppelin/data:/zeppelin/static_json`
  - `./zeppelin/jars:/zeppelin/jars`

## Construit avec

* Neo4j v3.4.10
* Apache Zeppelin v0.8.1
* Confluent Zookeeper
* Confluent Kafka
