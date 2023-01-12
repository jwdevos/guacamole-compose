.PHONY: default status bootstrap up down check_prune prune

COMPOSE_FILE="./docker-compose.yml"
DB_VOLUME_NAME="guacamole_guacdb_data"
DB_CONTAINER_NAME="guacamole-db"

default:
        @echo "USAGE: make <TARGET>"

status:
        docker ps -a
        docker volume ls

bootstrap:
        docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > initdb.sql
        docker compose -f $(COMPOSE_FILE) up -d $(DB_CONTAINER_NAME)
        sleep 10
        docker exec -it $(DB_CONTAINER_NAME) sh -c "cat initdb.sql | mysql -u root --password="" guacamole_db"
        docker compose -f $(COMPOSE_FILE) down

up:
        docker compose -f $(COMPOSE_FILE) up -d

down:
        docker compose -f $(COMPOSE_FILE) down

check_prune:
        @echo -n "Are you abso-fucking-lutely sure? [y/N] " && read ans && [ $${ans:-N} = y ]

prune: check_prune
        docker compose -f $(COMPOSE_FILE) down
        docker volume rm $(DB_VOLUME_NAME)
        rm initdb.sql
