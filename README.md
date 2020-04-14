# StatefulSet-Mongodb

Mongodb stateful set in GKE with 3 replicas 

Configuring replicas in mongodb:
```
> rs.initiate()
rs0:OTHER> var cfg = rs.conf()
rs0:PRIMARY> cfg.members[0].host="mongo-0.mongo:27017"
rs0:PRIMARY> rs.reconfig(cfg)
rs0:PRIMARY> rs.add("mongo-1.mongo:27017")
rs0:PRIMARY> rs.add("mongo-2.mongo:27017")
```

Exposing the mongodb:

```
kubectl expose pod mongo-0 --port 27017 --target-port 27017 --type LoadBalancer
kubectl expose pod mongo-1 --port 27017 --target-port 27017 --type LoadBalancer
kubectl expose pod mongo-3 --port 27017 --target-port 27017 --type LoadBalancer
```

Connecting to the mongodb ReplicaSet:

```
mongo mongodb://ip_for_mongo_replica_1:27017,ip_for_mongo_replica_2:27017,ip_for_mongo_replica_3:27017
```
