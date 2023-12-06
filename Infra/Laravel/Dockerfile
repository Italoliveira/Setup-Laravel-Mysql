FROM php:8.2-fpm-alpine

# Configure o diretório de trabalho
WORKDIR /var/www/localhost/htdocs

# Instale dependências necessárias para o Composer
RUN apk update && \
    apk add --no-cache curl unzip nginx

RUN docker-php-ext-install pdo_mysql

# Instale o Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN rm -rf /var/cache/apk/*

# Expor a porta 9000 (padrão do "php artisan serve")
EXPOSE 9000

COPY ./Infra/Nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./Infra/Nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --chown=root:www-data ./src /var/www/localhost/htdocs

RUN chown www-data:www-data -R /var/www/localhost/htdocs/storage

# Comando para iniciar o servidor embutido do Laravel
CMD ["php-fpm"]