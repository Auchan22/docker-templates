#!/bin/bash

DOCKER_BE = app

help: ## Show this help message
	@echo 'usage: make [target]'
	@echo
	@echo 'targets:'
	@egrep '^(.+)\:\ ##\ (.+)' ${MAKEFILE_LIST} | column -t -c 2 -s ':#'

start: ## Start the containers
	docker network create network-php-mysql || true
	cp -n docker-compose.yml.dist docker-compose.yml || true
	docker compose up -d

stop: ## Stop the containers
	docker compose stop

restart: ## Restart the containers
	$(MAKE) stop && $(MAKE) start

build: ## Rebuilds all the containers
	docker network create network-php-mysql || true
	cp -n docker-compose.yml.dist docker-compose.yml || true
	docker compose build

prepare: ## Runs backend commands
	$(MAKE) composer-install

# Backend commands
composer-install: ## Installs composer dependencies
	docker exec  ${DOCKER_BE} composer install --no-interaction
# End backend commands

ssh-be: ## bash into the be container
	docker exec -it ${DOCKER_BE} bash

code-style: 
	 docker exec ${DOCKER_BE} php-cs-fixer fix src 