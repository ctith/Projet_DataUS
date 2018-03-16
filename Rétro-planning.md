# Rétro-planning et tâches effectuées

## Du 5 au 15/03
1. Recherche de données US et FR sur le tabac

2. Installation de Kafka effectué :
- lors de l'installation d'Hadoop sur le cluster
- lors du TP kafka
```
wget http://apache.mindstudios.com/kafka/1.0.1/kafka_2.11-1.0.1.tgz
tar -xf kafka_2.11-1.0.1.tgz
```

## Le 16/03
1. Définition du projet et de son architecture : [Voir README.MD](https://github.com/ctith/Projet_DataUS/blob/master/README.md)

2. Création du repository git : [ICI](https://github.com/ctith/Projet_DataUS)

3. Transformation des données [csv](https://www.healthdata.gov/dataset/community-health-status-indicators-chsi-combat-obesity-heart-disease-and-cancer/resource) en [json](https://github.com/ctith/Projet_DataUS/tree/master/data/json)

4. Installation de MongoDB sur le cluster AWS : [ICI](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list

sudo apt-get update

sudo apt-get install -y mongodb-org

sudo service mongod start
cd /var/log/mongodb
cat mongod.log
> [initandlisten] waiting for connections on port 27017

mongo --host 127.0.0.1:27017
```
