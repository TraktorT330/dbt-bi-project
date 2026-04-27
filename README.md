# dbt-bi-project

dbt-проект для PostgreSQL и ClickHouse, запускаемый через Docker.

## Структура

- `Dockerfile` — multi-stage образ с `dbt-core`, `dbt-postgres`, `dbt-clickhouse`
- `docker-compose.yml` — запуск контейнера с volumes и env_file
- `profiles/profiles.yml` — подключения dbt (пароли через env_var)
- `projects/my_analytics/` — сам dbt-проект
- `.env.example` — шаблон секретов (реальный `.env` не коммитится)

## Деплой на сервере

```bash
git clone https://github.com/TraktorT330/dbt-bi-project.git
cd dbt-bi-project

cp .env.example .env
# отредактировать .env, вписать реальные пароли
chmod 600 .env

docker build --target dbt -t my-dbt .

docker compose run --rm dbt debug --target postgres_dev
docker compose run --rm dbt debug --target clickhouse_dev
```
