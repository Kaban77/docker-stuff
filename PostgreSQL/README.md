### Запуск
docker-compose up -d

При желании поменять название БД, логин и пароль

### Данные для подключения

- URL - jdbc:postgresql://localhost:5432/${POSTGRES_DB}
- User - ${POSTGRES_USER}
- Password - ${POSTGRES_PASSWORD}

### Обновление версии

* Обновить версию образа в `docker-compose.yml`
* Создать новый контейнер (`docker-compose up -d`)
* Сделать dump текущей БД

```
docker exec -t ${old_pg_container_id} pg_dumpall -c -U postgres > dump.sql
```

* Загрузить dump в новый контейнер

```
cat dump.sql | docker exec -i ${new_pg_container_id} psql -U postgres
```