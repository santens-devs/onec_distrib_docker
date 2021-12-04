# Пример использования

```shell
# Создадим контейнер с дистрибутивами 
docker create --name onec albus/onec:bin

# Добавим ссылку на нужный дистрибутив
docker create --name onec_8.3.17.2306 albus/onec:8.3.17.2306

# Можно запускать в работу
docker run --rm -it --volumes-from onec --volumes-from onec_8.3.17.2306 ubuntu ls -lha /opt/onec/platform/current/
```