# Пример использования

```shell
# Создадим контейнер с дистрибутивами 
docker create --name onec --net null albus/onec:bin

# Добавим ссылку на нужный дистрибутив
docker create --name onec_8.3.17.2306 --net null albus/onec:8.3.17.2306

# Можно запускать в работу
docker run --name crs --hostname crs --domainname lgss.local \
--volumes-from onec --volumes-from onec_8.3.17.2306 \
--workdir /opt/onec/platform/current --rm -it ubuntu env LC_ALL=C ./crserver
```
