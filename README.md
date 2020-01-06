# Redhat quay HA
```
https://github.com/quay/quay/blob/master/docs/development-container.md

# Architecture
 ![Quay HA](https://github.com/zhangchl007/quay-ha/blob/master/config/quayha01.png?raw=true）
 
# generate self certification 
self-cert-generate.sh test.com quay01.test.com quay02.test.com quay03.test.com registry.test.com

# Deploy Quay
# create Directory for Quay
sudo sh pre-quaydeploy.sh

# create the quayconfig container
sudo docker-compose  -f docker-compose.config.yml  up -d

# generate config file via web GUI
username/password: quayconfig/redhat
sudo mv quay-config.tar.gz  /quay/config
cd /quay/config && tar -zxvf quay-config.tar.gz

# delete the quayconfig container
sudo sh ./pre-deleteconfig.sh

# stop redis 
sudo docker-compose  -f docker-compose.config.yml stop

# Quay node01 redis and quay
sudo docker-compose  -f docker-compose.quayha.yml up -d

# Quay node02/node03 quay
sudo docker-compose -f docker-compose.quayha-noredis.yml up -d

# clean up Quay
sh clear-quay.sh

```
# quay-ha
