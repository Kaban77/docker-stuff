## Запуск
docker-compose up -d

## Интерфейс
http://localhost:8099/

## Авторизация

Для получения пароля администратора нужно зайти в контейнер:

```
docker exec -it ${container_id} /bin/bash
```

Далее смотрим пароль:

```
cat /nexus-data/admin.password
```

Логин - `admin`
Пароль - содержимое файла

При первой авторизации будет предложено поменять пароль.

## Подключение docker registry

- Создать репозиторий **docker(hosted)**
- На странице создания поставиль галочку http или https, указать порт **8082**
- Перейти во вкладку **Realms**, передвинуть в столбец Active строку **Docker Bearer Token**, нажать save
- При выполнении команд docker нужно обращаться к 8082 порту, или к тому, на который он перенаправляется (см. docker-compose.yml)

`docker login your_host:8082/your_registry`