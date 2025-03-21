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

## Создание Runner

- Сгенерить сертификаты (TODO)
- Выполнить следующие комманды в контейнере раннера, указав своё значение `hostname`:

  `SERVER=hostname`
  
  `PORT=443`
  
  `CERTIFICATE=/etc/gitlab-runner/certs/${SERVER}.crt`
  
  `mkdir -p $(dirname "$CERTIFICATE")`
  
  `openssl s_client -connect ${SERVER}:${PORT} -showcerts </dev/null 2>/dev/null | sed -e '/-----BEGIN/,/-----END/!d' | tee "$CERTIFICATE" >/dev/null`


- Добавить сертификат и ключ в контейнеры гилаба и раннера (названия файлов должны соответствовать `hostname`)
Для runner:

```
docker cp cert_name gitlab_runner_container_id:/etc/gitlab-runner/certs/cert_name
```

- Зарегистрировать раннер, указать необходимые значения: адрес гитлаба, токен для регистрации
(он находится в разделе `CI/CD Settings` -> `Runners` проекта, куда добавляется раннер).
В разделе `Enter an executor` указать `docker`

```
gitlab-runner register --tls-ca-file="$CERTIFICATE"
```

in progress
