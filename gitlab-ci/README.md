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
- Добавить сертификат и ключ в контейнеры гилаба и раннера (названия файлов должны соответствовать `hostname`)
Для runner:

```
docker cp cert_name gitlab_runner_container_id:/etc/ssl/certs/cert_name
```

- Открыть любой проект, зайти в `CI/CD Settings` -> `Runners`.
- Зайти в контейнер runner'а

```
docker exec -it gitlab_runner_container_id /bin/bash
```

Ignore SSL Error

SERVER=gitlab.rom.home
PORT=443
CERTIFICATE=/etc/gitlab-runner/certs/${SERVER}.crt
# Create the certificates hierarchy expected by gitlab
mkdir -p $(dirname "$CERTIFICATE")
# Get the certificate in PEM format and store it
openssl s_client -connect ${SERVER}:${PORT} -showcerts </dev/null 2>/dev/null | sed -e '/-----BEGIN/,/-----END/!d' | tee "$CERTIFICATE" >/dev/null
# Register your runner
gitlab-runner register --tls-ca-file="$CERTIFICATE"


- Выполнить комманду `gitlab-runner register --tls-ca-file="$CERTIFICATE"`, указать необходимые значения: адрес гитлаба, токен для регистрации
(он указан в гитлабе, в разделе runners, см выше)
- В разделе `Enter an executor` указать `docker`


in progress
