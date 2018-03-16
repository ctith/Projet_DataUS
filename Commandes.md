# Liste de commandes utilisés durant le projet

## Aller sur le cluster ubuntu AWS
```
ssh -i "NC_AWS_KEY.pem" ubuntu@IP_publique
```

## Lancer Kafka dans le dossier kafka
### Terminal 1: Démarrer zookeeper
```
./bin/zookeeper-server-start.sh ./config/zookeeper.properties
```
### Terminal 2 : Démarrer les serveurs (brokers) kafka
```
./bin/kafka-server-start.sh ./config/server.properties
```

## Lancer MongoDB
### Terminal 1 : Lancer le server MongoDB dans le dossier bin
```
mongod
```

### Terminal 2 : Lancer le client MongoDB au port 27017 dans le dossier bin
```
mongo
```
