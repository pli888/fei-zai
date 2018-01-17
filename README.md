# fei-zai
Testing Yii version 1 with LaraDock

## How to use

```bash
# Bring up Docker Ubuntu VM
vagrant up
# Change branch to yii2-docker or yii2-laradock
git checkout <name of branch>
# Clone submodule
git submodule init
git submodule update
# Create .env file
cd yii2-docker
cp .env-dist .env
# Spin up and log into VM
vagrant up
vagrant ssh
# Build containers
cd /vagrant/yii2-docker
docker-compose build
# Test
docker-compose run --rm php php /tests/requirements.php
```