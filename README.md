# fei-zai
Testing Yii with LaraDock

## Test Yii version 1 with yii2-laradock

```bash
# Stop all containers started by docker-compose
$ docker stop $(docker ps -a -q)
# Remove all containers
$ docker rm $(docker ps -a -q)
# Check
$ docker-compose ps
# Spin up and log into VM
$ vagrant up
$ vagrant ssh
# Build and start containers
$ cd /vagrant/yii2-laradock
$ docker-compose up -d nginx postgres pgadmin
# Check containers are running
$ docker-compose ps
# Log into workspace container
$ docker-compose exec --u=laradock workspace bash
# Use composer to download Yii version 1 from github
$ composer create-project --prefer-dist --stability=dev yiisoft/yii yii-1.1.16
# Test yii console command by creating a skeleton Yii application
$ cd yii-1.1.16/framework
$ chmod a+x yiic
$ ./yiic webapp ../testdrive
# Logout of workspace container
$ exit
# Log into nginx container
docker exec -it yii2laradock_nginx_1 bash
# Create nginx conf file
cd /etc/nginx/sites-available
cp app.conf.example yii_requirements.conf
# Make changes to yii_requirements.conf
$ vi yii_requirements.conf
server_name 192.168.42.10;
root /var/www/yii-1.1.16/;
# Reload nginx config
$ nginx -s reload
```

Check out:
* [http://192.168.42.10/requirements](http://192.168.42.10/requirements)
* [http://192.168.42.10/demos/blog/](http://192.168.42.10/demos/blog/)
* [http://192.168.42.10/demos/hangman/](http://192.168.42.10/demos/hangman/)
* [http://192.168.42.10/demos/helloworld/](http://192.168.42.10/demos/helloworld/)
* [http://192.168.42.10/demos/phonebook/](http://192.168.42.10/demos/phonebook/)


## Test yii2-laradock

Check out [documentation](https://github.com/ydatech/yii2-laradock/wiki/How-To-Install-Yii2-Framework-Basic-Template-on-Laradock)
in [yii2-laradock](https://github.com/ydatech/yii2-laradock).

```bash
# Start Docker Ubuntu VM
$ vagrant up
# Change branch
git checkout yii2-laradock
# Clone submodule
$ git submodule init
$ git submodule update
# Create .env file
$ cd yii2-laradock
$ cp env-example .env
# Make changes to .env if required
# Spin up and log into VM
$ vagrant up
$ vagrant ssh
# Build and start containers
$ cd /vagrant/yii2-laradock
$ docker-compose up -d nginx mysql
# Check containers are running
$ docker-compose ps
           Name                          Command              State                     Ports                  
---------------------------------------------------------------------------------------------------------------
yii2laradock_applications_1   /true                           Exit 0                                           
yii2laradock_mysql_1          docker-entrypoint.sh mysqld     Up       0.0.0.0:3306->3306/tcp                  
yii2laradock_nginx_1          nginx                           Up       0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
yii2laradock_php-fpm_1        docker-php-entrypoint php-fpm   Up       9000/tcp                                
yii2laradock_workspace_1      /sbin/my_init                   Up       0.0.0.0:2222->22/tcp  

# Log into workspace container
$ docker-compose exec --u=laradock workspace bash
# Use composer to download PHP dependencies into vendor directory
$ composer create-project --prefer-dist --stability=dev yiisoft/yii2-app-basic basic
$ cd basic
# Test yii console command
$ yii
# Logout of workspace container
$ exit
# Log into nginx container
docker exec -it yii2laradock_nginx_1 bash
# Create nginx conf file
cd /etc/nginx/sites-available
cp app.conf.example basic.conf
# Make changes to basic.conf
$ vi basic.conf
server_name 192.168.42.10;
root /var/www/basic/web;
# Reload nginx config
$ nginx -s reload
```

Check out [http://192.168.42.10](http://192.168.42.10) to see web page.