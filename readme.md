# step 1: generate key to set replica with algorithm

# openssl rand -base64 756 > mongo-keyfile

# chmod 400 mongo-keyfile

# step 2: exec into docker container

# docker exec -it mongo1 mongo -u root -p example --authenticationDatabase admin

# step 3: config replica at docker

rs.initiate( {
\_id : "replica0",
members: [
{ _id: 0, host: "mongo1:27017" },
{ _id: 1, host: "mongo2:27017" },
{ _id: 2, host: "mongo3:27017" }
]})

# step 4: exec into lits left container set slave by command

# rs.slaveOK()

# at master : create user by command

# db.createUser({user: "admin", pwd: "123123", roles: [{role: "root", db: "admin"}]})

# create role

# use admin

# db.createRole(

# {

# role: "user",

# privileges: [

# { resource: { cluster: true }, actions: [ "addShard" ] },

# { resource: { db: "config", collection: "" }, actions: [ "find", "update", "insert", "remove" ] },

# { resource: { db: "users", collection: "" }, actions: [ "update", "insert", "remove" ] },

# { resource: { db: "", collection: "" }, actions: [ "find" ] }

# ],

# roles: [

# { role: "read", db: "admin" }

# ]

# },

# { w: "majority" , wtimeout: 5000 }

# )
