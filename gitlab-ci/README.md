## Запуск
docker-compose up -d

## Авторизация
Открыть gitlab нужно по адресу, указанному в файле `docker-compose.yml` в параметре `hostname`

Логин `root`, для получения пароля нужно зайти в контейнер:

```
docker exec -it gitlab_container_id /bin/bash
```

Выполнить команду

```
cat /etc/gitlab/initial_root_password
```



in progress
