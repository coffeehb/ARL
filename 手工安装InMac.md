1、准备rabbitmq：
```
brew install rabbitmq
rabbitmqctl add_vhost arlv2host
rabbitmqctl add_user arl arlpassword
rabbitmqctl set_user_tags arl administrator
rabbitmqctl set_permissions -p arlv2host arl ".*" ".*" ".*"
rabbitmqctl delete_user guest
```
2、mongodb准备
```
mkdir -p /usr/local/var/log/mongodb
mkdir -p /usr/local/var/mongodb
mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
```
