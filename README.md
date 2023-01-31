# R4.03 Qualité et au delà du relationnel

Ce dépôt contient des ressources à destination des étudiants de seconde année de BUT Informatique à l'IUT d'Amiens.

## Utilisation

### Identifiants

MongoDB :

- login : `mongodb`
- password : `mongodb`

### UNIX / WSL2

Sous unix ou wsl2, vous pouvez utiliser la commande `make` pour démarrer et arrêter les conteneurs, vous pouvez consulter les commandes disponibles avec `make` ou `make help`.

> Vous aurez peut-être besoin d'installer make

### VM IUT

Ne tenez compte de ces instructions uniquement si vous êtes sur une VM de l'IUT.

Si vous êtes sur votre poste personnel, assurez-vous de remplir au moins une des conditions suivantes :

- Vous êtes connectés au réseau `upjv`
- Vous êtes connectés au VPN UPJV

Si vous remplissez ces conditions, vous pouvez utiliser SSH pour mapper un port de votre VM sur votre ordinateur à l'aide de la commande suivante :

```
ssh -L <port sur votre machine>:10.1.137.<votre IP de serveur>:<port sur le serveur> etudiant@10.1.137.<votre IP de serveur>
```

Pour transférer le port 8080 utilisé par readis, ça donnerait par exemple :

```
ssh -L 8080:10.1.137.121:8080 etudiant@10.1.137.121
```

### Systèmes Unix avec Make

Que votre ordinateur soit sous Unix ou que vous utilisiez le serveur de l'IUT, vous pouvez utiliser ces commandes make pour démarrer les différents SGBDs.

#### Redis

| Action               | Commande             |
|----------------------|----------------------|
| Démmarer le SGBD     | `make start-redis`   |
| Arrêter le SGBD      | `make stop-redis`    |
| Se connecter au SGBD | `make connect-redis` |

#### MongoDB

| Action               | Commande             |
|----------------------|----------------------|
| Démmarer le SGBD     | `make start-mongo`   |
| Arrêter le SGBD      | `make stop-mongo`    |
| Se connecter au SGBD | `make connect-mongo` |

#### Neo4j

| Action               | Commande                       |
|----------------------|--------------------------------|
| Démmarer le SGBD     | `make start-neo4j`             |
| Arrêter le SGBD      | `make stop-neo4j`              |
| Se connecter au SGBD | [Neo4j](http://127.0.0.1:7474) |

### Tous systèmes

L'ensemble des SGBD que l'on va utiliser sont portés sous docker, nous allons pour utiliser la commande `docker compose` (ou `docker compose` sur d'anciennes versions de Docker) pour les démarrés et arrêtés à notre guise, ainsi que pour lancer des shells pour s'y connecter.

#### Redis

| Action               | Commande                                                                                                   |
|----------------------|------------------------------------------------------------------------------------------------------------|
| Démmarer le SGBD     | `docker compose up -d redis readis phpredisadmin`                                                          |
| Arrêter le SGBD      | `docker compose up -d --scale redis=0 --scale readis=0 --scale phpredisadmin=0 redis readis phpredisadmin` |
| Se connecter au SGBD | `docker compose run rcli`                                                                                  |

#### MongoDB

| Action               | Commande                                                                           |
|----------------------|------------------------------------------------------------------------------------|
| Démmarer le SGBD     | `docker compose up -d mongo mongo-express`                                         |
| Arrêter le SGBD      | `docker compose up -d --scale mongo=0 --scale mongo-express=0 mongo mongo-express` |
| Se connecter au SGBD | `docker compose run mgcli`                                                         |

#### Neo4j

| Action               | Commande                                                     |
|----------------------|--------------------------------------------------------------|
| Démmarer le SGBD     | `docker compose up -d neo4j`                                 |
| Arrêter le SGBD      | `docker compose up -d --scale neo4j=0 neo4j`                 |
| Se connecter au SGBD | [http://127.0.0.1:7474](http://127.0.0.1:7474)               |

## Outils

Nous avons à disposition plusieurs IHM en mode web pour différents SGBDs

| SGBD       | Lien                                                                                                                     |
|------------|--------------------------------------------------------------------------------------------------------------------------|
| Redis      | Readis [http://127.0.0.1:8080/](http://127.0.0.1:8080/) - phpRedisAdmin [http://127.0.0.1:8081/](http://127.0.0.1:8081/) |
| MongoDB    | MongoExpress [http://127.0.0.1:8082](http://127.0.0.1:8082)                                                              |
| Neo4j      | Neo4j [http://127.0.0.1:7474](http://127.0.0.1:7474)                                                                     |

Attention pour Neo4j, si vous utilisez le serveur de l'IUT vous aurez besoin de mapper les ports `7474` et `7687` à votre PC.
