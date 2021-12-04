# Сборка контейнера

Для начала нужно собрать пустой контейнер

```sh
docker build -t albus/onec:bin --file ./DockerFile --disable-content-trust .
```

# Схема расположения дистрибутивов

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICAvb3B0L29uZWMvOCAtLT4gMTdcbiAgICAvb3B0L29uZWMvOCAtLT4gMThcbiAgICAvb3B0L29uZWMvOCAtLT4gMTlcblxuXG4gICAgMTcgLS0-IDIyNTYveDg2XzY0XG4gICAgMTcgLS0-IDIzMDYveDg2XzY0XG5cbiAgICAxOCAtLT4gMTY5Ni94ODZfNjRcbiAgICAxOSAtLT4gMTQxNy94ODZfNjQiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOnRydWUsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)](https://mermaid.live/edit#eyJjb2RlIjoiZ3JhcGggVERcbiAgICAvb3B0L29uZWMvOCAtLT4gMTdcbiAgICAvb3B0L29uZWMvOCAtLT4gMThcbiAgICAvb3B0L29uZWMvOCAtLT4gMTlcblxuXG4gICAgMTcgLS0-IDIyNTYveDg2XzY0XG4gICAgMTcgLS0-IDIzMDYveDg2XzY0XG5cbiAgICAxOCAtLT4gMTY5Ni94ODZfNjRcbiAgICAxOSAtLT4gMTQxNy94ODZfNjQiLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjp0cnVlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)

# Добавление нового дистрибутива

Нам нужно добавить в образ новый слой с дистрибутивом.

Создадим контейнер
```sh
docker create --name onec albus/onec:bin
```

Скопируем в него дистрибутив
```sh
docker cp ./opt/1C/8.3/x84_64 onec:/opt/onec/8/3/17/3456/
```

Зафиксируем слой в образе при этом нужно создать том подключения для монтирования данного дистрибутива
```sh
docker commit --change "VOLUME /opt/onec/8/3/17/3456/x86_64" --message "add 8.3.17.3456" onec albus/onec:bin
```

Теперь образ можно поместить в репозиторий, а контейнер использовать как общие тома
```sh
docker run -it --rm --volumes-from onec ubuntu ls -lha /opt/onec/8/3/17/3456/x86_64
```

# Использование контейнера

```sh
docker create --name onec albus/onec:bin
docker run -it --rm --volumes-from onec ubuntu ls -lha /opt/onec/8/3/17/3456/x86_64
```
