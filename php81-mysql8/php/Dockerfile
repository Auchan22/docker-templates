FROM php:8.1-fpm-alpine

# # Pasamos como argumento, el user_id
# ARG UID

# # Creamos un usuario dentro del contenedor con el user_id recibido por argumento, haciendolo superuser (tema permisos)
# RUN adduser -u ${UID} --disabled-password --gecos "" appuser
# RUN mkdir /home/appuser/.ssh
# RUN chown -R appuser:appuser /home/appuser/
# RUN echo "StrictHostKeyChecking no" >> /home/appuser/.ssh/config
# RUN echo "alias sf=/appdata/www/bin/console" >> /home/appuser/.bashrc

# USER appuser

# Se instalan extensiones correspondientes a MySQL
RUN docker-php-ext-install pdo pdo_mysql 

# allow super user - set this if you use Composer as a
# super user at all times like in docker containers
ENV COMPOSER_ALLOW_SUPERUSER=1

# obtain composer using multi-stage build
# https://docs.docker.com/build/building/multi-stage/
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

# Copiando archivos de composer (json y lock), antes de hacer el composer install
# This is enough to take advantage of docker cache and composer install will
# be executed only when composer.json or composer.lock have indeed changed!-
# https://medium.com/@softius/faster-docker-builds-with-composer-install-b4d2b15d0fff
COPY ./app/composer.* ./

# Install PHP-CS-FIXER
RUN wget https://cs.symfony.com/download/php-cs-fixer-v3.phar -O php-cs-fixer
RUN chmod a+x php-cs-fixer
RUN mv php-cs-fixer /usr/local/bin/php-cs-fixer

# Instalación y update
RUN curl https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer
RUN composer self-update

# Copiar los archivos locales al contenedor
COPY ./app .

# Comando para optimizar composer
RUN composer dump-autoload --optimize