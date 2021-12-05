# Пример использования

## Создадим контейнер с дистрибутивами 
```shell
docker create --name onec --net null albus/onec:bin
```
## Добавим ссылку на нужный дистрибутив
```shell
docker create --name onec_8.3.17.2306 --volumes-from onec:ro --net none albus/onec:8.3.17.2306
```

## Можно запускать в работу
```shell
docker run --name crs --hostname crs --domainname lgss.local \
--volumes-from onec_8.3.17.2306:ro \
--publish 1542:1542/tcp --publish 1542:1542/udp --publish 21542:22/tcp \
--ulimit nofile=262144:262144 --restart always --detach \
--volume /usr/share/ros/oem/crs/1542:/shares/crs/1542:consistent \
albus/baseimage:master /sbin/my_init -- env LC_ALL=C /opt/onec/platform/current/crserver -port 1542 -d /shares/crs/1542
```
