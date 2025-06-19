# loki-s3-minio

## Подготовка

Для сбора логов docker-контейнеров требуется установить драйвер `Loki`.
```shell
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```

После чего нужно добавить в конфигурацию `/etc/docker/daemon.json` настройки для отправки логов в `Loki`.

```json
{
    "debug" : true,
    "log-driver": "loki",
    "log-opts": {
        "loki-url": "http://127.0.0.1:3100/loki/api/v1/push"
    }
}
```

Перезапускаем docker.

```shell
service docker restart
```

## Запуск

```bash
docker compose up -d
```

## Grafana

В `grafana` установлен плагин `grafana-lokiexplore-app` в панели `Drilldown`, который позволяет удобно просматривать логи по лейблам без использования языка LogQL.

Больше информации на сайте https://grafana.com/docs/grafana/latest/explore/simplified-exploration/logs/.