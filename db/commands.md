# Connect to primary node
docker-compose exec mongo-primary mongo -u "yoda" -p "030888"

# Instantiate the replica set
rs.initiate({"_id" : "db-replica-set","members" : [{"_id" : 0,"host" : "mongo-primary:27017"},{"_id" : 1,"host" : "mongo-worker-1:27017"},{"_id" : 2,"host" : "mongo-worker-2:27017"},{"_id" : 3,"host" : "mongo-worker-3:27017"}]});

## Set the priority of the master over the other nodes
conf = rs.config();
conf.members[0].priority = 2;
rs.reconfig(conf);

# Create a cluster admin
use admin;
db.createUser({user: "luke",pwd: "030888",roles: [ { role: "userAdminAnyDatabase", db: "admin" },  { "role" : "clusterAdmin", "db" : "admin" } ]});
db.auth("luke", "030888");

# Create a collection on a database
use daf;
db.createUser({user: "leia",pwd: "030888",roles: [ { role: "readWrite", db: "daf" } ]});
db.createCollection('places');
db.createCollection('users');

# Verify credentials 
docker-compose exec mongo-primary mongo -u "leia" -p "030888" --authenticationDatabase "daf"