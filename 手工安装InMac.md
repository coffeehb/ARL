本地环境：Mac OSX

# 基础配置
## rabbitmq
brew install rabbitmq
rabbitmqctl add_vhost arlv2host
rabbitmqctl add_user arl arlpassword
rabbitmqctl set_user_tags arl administrator
rabbitmqctl set_permissions -p arlv2host arl ".*" ".*" ".*"
rabbitmqctl delete_user guest

## Mongodb

mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
初始化：
use arl
db.user.drop()
db.user.insert({ username: 'admin',  password: hex_md5('arlsalt!@#'+'arlpass') })

## Nginx 80
cp nginx.conf /usr/local/etc/nginx/nginx.conf
Mac 自带nginx 启动

## ARL - 5003端口

gunicorn -b 0.0.0.0:5003 app.main:arl_app -w 3 --access-logfile arl_web.log

## 启动worker


sudo celery -A app.celerytask.celery worker -l info -Q arltask -n arltask -c 2 -O fair -f arl_worker.log
